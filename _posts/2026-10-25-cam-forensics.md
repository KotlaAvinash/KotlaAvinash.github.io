---
title: "My PC was keeping a diary of every app that used my camera. Then I almost erased it."
date: 2026-10-25
categories: [DFIR, Forensics]
tags: [Windows, Forensics, DFIR, SQLite, Camera, Microphone, Capability Access Manager, CAMtool, Digital Forensics, Incident Response]
image:
  path: /assets/img/posts/cam-forensics/banner.png
  alt: Windows Capability Access Manager — the hidden diary of every app that used your camera and mic
---

*How Windows quietly logs every app that uses your camera and microphone — and how I nearly destroyed the evidence by opening it the normal way.*

---

It started with a folder I had never noticed before.

I was poking around a Windows 11 machine, looking at the usual forensic places, when I saw this:

`C:\ProgramData\Microsoft\Windows\CapabilityAccessManager\`

Inside were a few small files with long names, ending in `.db`. Databases. Sitting quietly next to the operating system.

So of course I had to open them.

---

## Wait… Windows tracks this?

Turns out, yes. Windows has a service called the **Capability Access Manager** that stands between apps and your private stuff: camera, microphone, location, contacts, screen capture, even passkeys. And on Windows 11 it keeps a database.

When an app wants one of those, Windows checks your privacy settings, decides Allow / Deny / Ask, and then it **writes it down.**

Which app. Which feature. When it started. When it stopped. Which user account. And for normal desktop programs, the **full path of the .exe** plus its file hash.

That little camera or mic icon in your taskbar? This is its memory.

![Four files, one quiet diary](/assets/img/posts/cam-forensics/02_where_it_lives.png)
*Four files, one quiet diary*

There are two main files:

- **CapabilityAccessManager.db**: the diary. Who used what, and when.
- **CapabilityConsentStorage.db**: the rules. Your Allow / Deny / Prompt switches for every app.

Plus two helper files (`-wal` and `-shm`) that turned out to matter much more than I expected. More on that in a minute.

For an investigator, this is gold. *Was the webcam on during that meeting? Did some unknown program listen through the mic at night? Did it run from the Downloads folder?* The diary can answer that.

---

## The scary part

Here's where I made the mistake almost everyone makes.

I had a copy of the files (thankfully just a copy), and I opened it the "normal" way, with a regular SQLite library. The way you'd open any database.

The data looked fine. Then I checked the file again.

**It had shrunk from 1,048,576 bytes to 65,536 bytes.**

![I opened the database the normal way. The deleted records were gone.](/assets/img/posts/cam-forensics/03_evidence_vanished.png)
*I opened the database the normal way. The deleted records were gone.*

What happened? When SQLite opens a database, it quietly "tidies up". It merges the pending changes from the `-wal` file into the main file, and it trims the file down to the size the data needs.

But the end of that file wasn't empty. It held **old pages with 174 deleted records**: usage history that Windows had already "cleaned up", still sitting there in the bytes. One click, and they were gone.

My originals were safe because I never touch originals. But it changed how I looked at this whole thing:

> **Opening evidence the normal way can destroy evidence.**
{: .prompt-danger }

From then on, I only read the raw bytes myself and let SQLite touch throwaway copies, never the evidence.

---

## The newest activity wasn't even in the database

The next surprise: the main `.db` file was not up to date.

SQLite keeps recent changes in the **`-wal` file** (write-ahead log) and copies them into the `.db` later. So the latest uses (the evening right before the files were copied) existed **only in the -wal**.

Then I found one more full transaction in the **leftover disk space after the end of the -wal file**. It had been written while the files were being copied.

![Three layers: saved history, not saved yet, and even further](/assets/img/posts/cam-forensics/04_hidden_in_wal.png)
*Three layers: saved history, not saved yet, and even further*

So a tool that reads only the `.db` misses the most recent activity. And a tool that mixes all three layers together can't tell you where each row came from. I wanted both: read everything, but **label everything.**

---

## Two more traps

**1. Windows reuses IDs.** The database stores names like "Brave Browser" in small lookup tables, referenced by number. When Windows cleans up old rows, those numbers can later be given to new apps. My first version happily labelled some old *deleted* rows as "Brave Browser", for apps that were clearly not Brave. Now, if the original name is gone, the tool says **"unknown app (purged)"** instead of guessing.

**2. Permissions are "now", not "then".** The consent database stores your *current* setting, not its history. And a "Deny" at the system level beats an "Allow" on the app. So the tool shows it as **"Current setting: Deny (System default)"**, not "allowed by…", which would be a lie.

(I checked the Allow / Deny / Prompt values against the real Windows registry: 186 out of 186 matched.)

---

## So I built a tool for it: CAMtool

I wanted one simple thing: **open a report and immediately see who used what, when.**

![The activity timeline in CAMtool, on demo data](/assets/img/posts/cam-forensics/timeline.png)
*The activity timeline in CAMtool, on demo data*

CAMtool reads the databases, the `-wal`, the slack space and deleted records, without ever changing the original files. It hashes every file before and after the run to prove that. Then it builds a single report you can open in any browser:

- **A timeline:** every use, in order, with start, end, duration, app, full path, service, account, and Allowed / Blocked
- **App cards:** what each app used, how often, for how long

![Every application, one card each](/assets/img/posts/cam-forensics/applications.png)
*Every application, one card each*

- **Recovered records:** deleted rows brought back, clearly marked so they never mix with live data

![Deleted records, recovered and labelled](/assets/img/posts/cam-forensics/recovered.png)
*Deleted records, recovered and labelled*

- **Permissions**, **desktop programs** (with a flag for anything run from Temp, Downloads or another drive), an **Excel** export, and a small **desktop window** if you don't like the command line

> *All screenshots here use made-up demo data: a fake user called "analyst" and an invented case where an unknown `recorder.exe` from Downloads used the microphone for 2 hours at 2 AM, then got blocked from the camera a minute later.*
{: .prompt-info }

It's plain Python with nothing to install. Before calling it done, I hit it with 6,000+ corrupted files to make sure it never crashes on broken evidence, and fed it a million-row database to check it scales. A separate reviewer then went through the code, which caught a real security bug in the report that I fixed before release.

---

## Try it yourself

It's free and open source:

👉 **[github.com/whitedevil1026/CAMtool](https://github.com/whitedevil1026/CAMtool)**

```bash
python docs/demo/build_demo_evidence.py demo_evidence
python camtool_cli.py demo_evidence -o demo_report --tz +05:30
```

Open `demo_report/CAM_report.html` and explore the demo case. Or point it at a folder with a real `CapabilityAccessManager.db` (always a copy!).

---

## What I learned

- **Windows quietly records far more than most people think.** Camera, mic and location history sit in a plain database.
- **The "normal" way of opening evidence can destroy it.** Work on copies. Read the bytes.
- **The newest activity often isn't where you expect.** Always check the `-wal`.
- **Never guess.** If a tool doesn't know something, it should say so.

I started by opening a random folder. I ended up with a tool, and a lot more respect for what's hiding in plain sight on our own computers.

If you work in DFIR or just like digging into Windows, give it a try and tell me what you find. 🔍
