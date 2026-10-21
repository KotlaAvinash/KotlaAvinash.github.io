---
title: "Your phone left the PC. Its footprints didn't."
date: 2026-10-21
categories: [DFIR, Forensics]
tags: [Windows, Forensics, DFIR, PhoneLink, SQLite, Android, Artifacts, Digital Forensics, Incident Response]
image:
  path: /assets/img/posts/phone-link-forensics/banner.png
  alt: Microsoft Phone Link — What it leaves behind on Windows
---

*What Microsoft Phone Link leaves behind on Windows, and why it matters for digital forensics*

---

If you've ever linked your phone to a Windows PC, that PC has been keeping notes.

I spent the last few weeks reading those notes. On one laptop I could see the phone's text conversations, its call history, its contacts, and a list of its photos by name and date. I could even tell which phones had been connected to that computer over time, including ones that were no longer linked.

All of it came from one app that ships with Windows: **Phone Link**. And none of it needed the phone.

Here's what I learned, written for anyone who has ever linked a phone to a PC, and for anyone who might one day need to investigate one.

---

## Your PC isn't looking at your phone. It's keeping a copy.

Most people think Phone Link works like a window: you look through the PC and see the phone.

That's not what happens.

![The phone sends copies to the PC, and the PC saves them in its own database files.](/assets/img/posts/phone-link-forensics/01-how-it-works.png)
*The phone sends copies to the PC, and the PC saves them in its own database files.*

When you pair the two, both sign in to the same Microsoft account and swap security certificates, so they recognise each other later. From then on, whenever they can reach each other (nearby over Bluetooth or Wi-Fi, or through Microsoft's cloud when they can't), the phone sends **copies** of its data to the PC.

The PC saves those copies into small database files on its own disk. That's why Phone Link still shows your recent texts when your phone is switched off. The PC isn't asking the phone. It's reading its own copy.

And a copy is something you can examine.

---

## One folder for every phone, and it stays

This was the part that surprised me most.

Every phone that is linked gets **its own folder** on the PC, named after an ID for that phone. Inside it are that phone's databases.

![Each phone ever linked leaves its own folder. Unlinking doesn't remove it.](/assets/img/posts/phone-link-forensics/02-one-folder-per-phone.png)
*Each phone ever linked leaves its own folder. Unlinking doesn't remove it.*

When you unlink a phone, or Phone Link clears its data, **the folder itself stays behind**. Sometimes it still has data, sometimes the databases are empty, and sometimes only the bare folder is left. But it's there.

That gives an investigator something valuable:

- **How many phones** were ever linked to that PC through Phone Link
- **Roughly when** each one was first linked, from the folder's creation date
- For linked phones, **which phone it was**: Phone Link keeps the make, model and Android version in a separate details file

So even when the data is gone, the PC still remembers that a phone was there.

---

## What's inside each phone's folder

Phone Link keeps **one database file per feature**. Here's a simple tour:

![One small database per feature, all inside the phone's folder.](/assets/img/posts/phone-link-forensics/03-what-each-database-holds.png)
*One small database per feature, all inside the phone's folder.*

- **phone.db**: text messages, picture messages and chat messages, the list of conversations, the phone's own number and carrier, and any messages typed on the PC but not yet sent
- **calling.db**: the call log, with who, incoming or outgoing or missed, when, and for how long
- **contacts.db**: the address book, including a small record when a number or email is deleted
- **photos.db**: the list of photos, with name, date taken, size and where each one sits on the phone
- **notifications.db**: the phone's notifications, including the chat messages shown inside them and even the reply buttons
- **phoneapps.db**: the apps installed on the phone
- A separate apps file records apps that were **opened in a window on the PC**, which is strong proof that someone actually used them on that computer
- Smaller files hold phone browser history and "continue on PC" items, the wallpaper, and Phone Link settings

> One thing to keep in mind: **these files don't link to each other.** A number in the call log is just text. Matching it to a name in the contacts is the investigator's own work, and a good report says so.
{: .prompt-warning }

---

## The traces outlive the content

Phone Link doesn't keep everything forever. Microsoft says it shows roughly the last month of text messages, the last three months of calls, and your most recent photos. When something gets too old, the row is deleted.

But "deleted" doesn't mean gone.

![Content expires, but traces stay behind.](/assets/img/posts/phone-link-forensics/04-what-survives.png)
*Content expires, but traces stay behind.*

- **Conversations outlive their messages.** The list of conversations stays long after the message text has expired. You may not know *what* was said, but you can still show *who* was in contact.
- **Photos leave their details.** The PC keeps a photo's name, date and size even when it doesn't hold the picture itself, which is enough to prove the photo existed.
- **Deleted notifications can come back.** These databases mark deleted rows as free space instead of wiping them. Until that space is reused, the old notification is still in the file and can be recovered.

---

## How the data is saved, and how easy it is to damage

This part matters most if you're the one handling the evidence.

![New data goes into a side file first. Copy all three files together.](/assets/img/posts/phone-link-forensics/05-how-data-is-saved.png)
*New data goes into a side file first. Copy all three files together.*

Phone Link's databases don't write new data straight into the main file. They write it to a small **side file** first (ending in `-wal`), and fold it into the main `.db` file later, usually when the app closes.

That leads to two simple rules:

> **Always copy the three files together:** `.db`, `-wal` and `-shm`. On a computer that's still running, the newest data may exist only in the side file. Copy the main file alone and you can get a perfectly valid, completely empty database.
{: .prompt-danger }

> **Never open the originals.** Double-clicking a database to "just take a look" opens it in a normal database program, which can merge and delete that side file when it closes. It happened to me: supporting files disappeared from an evidence folder after a quick double-click. I only got them back because I had made hash-checked copies earlier.
{: .prompt-danger }

---

## When was the phone there?

This is usually the first question in any case.

- **When it was linked:** the creation date of that phone's folder, plus the registration time in Phone Link's phone-details file. A small trap: Microsoft spelled that field `RegitrationTime`, so searching for "RegistrationTime" finds nothing.
- **When it last sent data:** the newest "last updated" time inside the databases. Those times come from the PC's own clock and mark when data last arrived from the phone.
- **One to be careful with:** the details file also has a "last seen" time. In my testing it didn't move after pairing, so it isn't proof of a later connection.

> When you first link a phone, Phone Link pulls in a chunk of older history in one go. A freshly linked phone can show weeks of calls on its very first day. So before saying how far back the data goes, check **when** the phone was linked.
{: .prompt-warning }

---

## If you remember only five things

1. Phone Link keeps a **copy** of the phone's data on the PC, not a live view.
2. Every phone ever linked leaves **its own folder**, even after it's unlinked.
3. Old content expires, but **traces stay behind**: conversation lists, photo details and deleted rows.
4. Check **when the phone was linked** before talking about how far back the data goes.
5. **Copy all three files, and never double-click the originals.**

---

Your phone might be in a drawer, or long gone. The PC it was once linked to may still be telling its story.

**Have you ever looked at what Phone Link leaves on a PC? I'd love to compare notes, especially on other phones and Windows versions.**

---

*Findings come from studying Phone Link on Windows 11 with an Android phone. Microsoft doesn't publish the layout of these files, so test anything here on your own case before relying on it.*
