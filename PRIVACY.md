# Privacy Policy — Panna

**Last updated: 2 October 2026**

Panna is a private diary for Windows. This policy describes what the app does with your information. It is short because the app does very little with it.

---

## The short version

**Panna does not collect anything, and it has no servers.**

Everything you write stays in a file on your own PC, encrypted with a key derived from your master password.

The one thing that can leave your PC without you choosing a destination each time is **Google Drive backup** — and only if you turn it on by signing in to your own Google account. What is uploaded is already encrypted; Google stores it and cannot read it. It is described in full below.

---

## What we collect

Nothing.

- No account, no sign-up, no email address
- No analytics, no telemetry, no crash reporting
- No advertising, no advertising identifiers
- No cookies
- No usage statistics of any kind

We do not have servers that could receive your data. **Unless you sign in to Google Drive backup, Panna makes no network requests at all.** If you do, it talks to Google and to nobody else.

---

## What the app stores, and where

All of it is on your own computer, in your Windows user profile:

| What | Where |
|---|---|
| Your entries | `%APPDATA%\Panna\diary.db` — encrypted |
| Photos and files you attach | `%APPDATA%\Panna\attachments\` — each file encrypted separately |
| Your wrapped encryption key | `%APPDATA%\Panna\vault.json` |
| A picture of your own behind the journal, or on the page | `%APPDATA%\Panna\background.bin`, `page.bin` — encrypted |
| Your Google sign-in, if you use Drive backup | `%APPDATA%\Panna\cloud.bin` — encrypted |
| Appearance settings, reminder time, backup schedule | `%APPDATA%\Panna\preferences.json` — not encrypted, contains no diary content |

Nobody else can read anything in this list except the last line without your master password or the answer to your security question.

Your name and profile picture, if you add them, are kept the same way — encrypted, in `profile.bin` and `avatar.bin`.

---

## How the encryption works

We publish this because a privacy claim you cannot check is worth nothing.

1. Your **master password** is put through **Argon2id** (memory-hard, deliberately slow) to produce a key-encryption key.
2. A separate, random **256-bit data encryption key** is generated once, on first run. This is what actually encrypts your diary.
3. The data key is sealed with **AES-256-GCM** under the key-encryption key, and only the sealed form is written to disk.
4. The answer to your **security question** seals a second copy of the same data key, through the same Argon2id step. That is how "Reset password" works: a right answer opens that copy, and the key is sealed again under the new password you choose. Nothing in the diary is re-encrypted or sent anywhere to do it.

The security question itself is stored unencrypted, because it has to be shown before the diary is unlocked. The answer is never stored. Be aware that this makes your diary only as private as that answer: someone who can use your PC and knows or guesses it can reset your password. Choose an answer people around you would not know. After five wrong answers the app makes you wait before trying again.

Diaries created before security questions were added were given a 24-word recovery phrase instead; it still works for resetting the password on those.

The unsealed data key exists only in memory, only while the app is unlocked, and is wiped when you lock it or close the app. It is never written to disk in usable form and never leaves the application process.

**This means we cannot recover your diary.** If you forget both your master password and the answer to your security question, the data is gone. There is no reset link that goes through us, and no support request will help. That is what makes it private.

---

## When information leaves your PC

Only when you explicitly ask for it, and only to where you choose:

- **Export** (PDF, Markdown, HTML, JSON) — writes a **decrypted** copy to the folder you pick. Anyone who can read that file can read your diary. Keep it somewhere safe or delete it when you are done.
- **Backup** (`.diarybak`) — stays encrypted. It can only be opened with the master password it was made under.
- **Save a copy** of an attachment — writes that one file, decrypted, where you choose.

Each of these requires you to open a dialog and choose a destination.

### Google Drive backup — optional, off until you sign in

If you choose **Sign in with Google** in Settings, Panna keeps copies of your diary in your own Google Drive.

- **What is uploaded:** the same `.diarybak` a local backup writes. It is encrypted on your PC, before it leaves, with your diary's own key. Google receives ciphertext. Neither Google nor we can open it — only your master password can.
- **Where it goes:** a folder named "Panna Backups" in your Drive. You can see it, download from it, or delete it there yourself at any time.
- **What Panna can see in your Drive:** only files it created. It asks Google for the narrowest permission available (`drive.file`) and cannot list, read, or change anything else you keep there.
- **What Panna learns about you:** your Google account's email address, shown in Settings so you know which Drive is in use. It is stored only on your PC, encrypted, and is never sent to us — we have nowhere to receive it.
- **Your Google password:** never seen by Panna. Sign-in happens on Google's own page in your browser.
- **When it runs:** when you press "Back up now", and automatically on the schedule you pick (daily, weekly, or never), while your diary is unlocked. This is the one thing Panna does in the background.
- **Turning it off:** "Sign out" in Settings removes the sign-in from your PC and tells Google to revoke the access. Backups already in your Drive stay there until you delete them. You can also remove Panna's access at any time from your Google Account's security settings.

Panna's use of information received from Google APIs adheres to the [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy), including the Limited Use requirements. That information is used only to provide the backup feature described here. It is not shared, sold, used for advertising, or read by any person.

---

## Permissions the app requests

Panna is a full-trust Windows desktop application packaged as MSIX. It uses the network for one purpose only — Google Drive backup, if you turn it on — and it reads and writes files only in its own folder or where you explicitly point it through a file dialog.

It shows local desktop notifications for the daily reminder, if you turn that on. These are generated on your PC by the app itself and are not sent through any service.

---

## Children

Panna is a general-purpose writing tool. Nothing you write is shared with anyone, and it has no communication features. It collects no information from anyone, including children.

---

## Changes to this policy

Google Drive backup is the first feature that uses the network, and it follows the rule we set for all of them: **off by default**, started only by you, and described here before it shipped. Any later one — weather, or an optional online AI service — will be handled the same way, and will state plainly what it sends and where.

---

## Contact

Questions about this policy or about the app:

**suryashastri36@gmail.com**

---

_Panna is not affiliated with, endorsed by, or connected to any other diary or journaling application._
