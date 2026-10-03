---
title: "Set up your email"
description: "How to connect a mailbox hosted by Vangera Systems to Outlook, iPhone, Android, Thunderbird or webmail — settings, step-by-step guides and security tips."
---

Your mailbox works with any modern email app. Most apps configure themselves when you enter your email address and password; if yours asks for settings, use the ones below.

## Server settings

| | Server | Port | Security |
|---|---|---|---|
| **Incoming mail (IMAP)** — recommended | `mail.lohn.cc` | **993** | SSL/TLS |
| **Outgoing mail (SMTP)** | `mail.lohn.cc` | **465** | SSL/TLS |
| Outgoing mail (alternative) | `mail.lohn.cc` | 587 | STARTTLS |
| Incoming mail (POP3, only if you really need it) | `mail.lohn.cc` | 995 | SSL/TLS |

- **Username:** your full email address, for example `name@yourcompany.com`.
- **Password:** your mailbox password — or, better, an **app password** (see below).
- Outgoing mail always requires signing in with the same username and password.

## Webmail

Open **[mail.lohn.cc/SOGo](https://mail.lohn.cc/SOGo)** in any browser for mail, calendar and contacts — nothing to install.

## Microsoft Outlook

**Outlook for Windows (Microsoft 365, 2021, 2019, 2016)**

1. **File → Add Account**.
2. Enter your email address and click **Connect**.
3. If Outlook asks for the account type, choose **IMAP**.
4. Enter your password (or app password) and click **Connect**. Outlook finds the server settings automatically.

**New Outlook for Windows, and Outlook for Mac**

1. Open **Settings → Accounts → Add account**.
2. Enter your email address. When asked for the provider, choose **IMAP**.
3. Open the advanced/manual settings and enter the server settings above.

**Outlook app for iPhone and Android**

1. **Add account → Add email account**, enter your address.
2. Choose **IMAP** (you may need to tap *Set up account manually*).
3. Enter the server settings above.

> The new Outlook for Windows and the Outlook mobile app sync IMAP mailboxes through Microsoft's cloud, which stores your login there. We recommend using an **app password** for them.

## iPhone, iPad and Mac (Apple Mail)

*Easiest — one-tap profile:* on your iPhone, iPad or Mac, open **[mail.lohn.cc](https://mail.lohn.cc/)** in Safari, sign in with your email address and password, and download the **Apple connection profile** (choose the version *with app password*). Open the downloaded profile in **Settings** and install it. Mail, calendar and contacts are set up for you, with a separate app password for that device. Don't share the profile file — it grants access to your mailbox.

*Or as an Exchange account (mail, calendar and contacts):*

1. **Settings → Mail → Accounts → Add Account → Microsoft Exchange** (on newer iOS: **Settings → Apps → Mail → Mail Accounts**).
2. Enter your email address and a description, tap **Next**, then **Configure Manually**.
3. Enter your password. If asked for a server, enter `mail.lohn.cc` and your full email address as the username.
4. Choose what to sync: Mail, Contacts, Calendars.

*Mail only:* choose **Other → Add Mail Account**, then **IMAP**, and use the server settings above.

## Android

*Gmail app (mail only):* **Settings → Add account → Other**, enter your address, choose **Personal (IMAP)**, then enter the server settings above.

*Mail, calendar and contacts:* in your phone's email app choose **Exchange** (or *Exchange and Microsoft 365*), enter your email address and password, and `mail.lohn.cc` as the server if asked.

## Thunderbird

1. **Account Settings → Account Actions → Add Mail Account**.
2. Enter your name, email address and password, then **Continue**.
3. Thunderbird finds the settings automatically (IMAP 993 and SMTP 465, both SSL/TLS). Click **Done**.

## Calendar and contacts

| App | Calendar & contacts |
|---|---|
| Webmail (SOGo) | Built in |
| iPhone / Android (Exchange account) | Synced automatically |
| Outlook for Windows (classic) | Use the free *Outlook CalDav Synchronizer* add-in, or webmail |
| Thunderbird | Built in (CalDAV/CardDAV address: `https://mail.lohn.cc/SOGo/dav/`) |

## Keep your mailbox secure

- **Use app passwords for devices.** Sign in at **[mail.lohn.cc](https://mail.lohn.cc/)** with your email address, open **App passwords**, and create one for each phone or computer. If a device is lost, revoke just that password — your main password stays safe.
- **Turn on two-factor authentication** for webmail in the same place.
- **Never share your password by email or chat.** Vangera Systems will never ask you for it.
- Prefer **IMAP** over POP3, so your mail stays in sync across all your devices and is included in the server's backups.

## Need help?

Email **[info@vangera.systems](mailto:info@vangera.systems)** or use the [contact form](/#contact). Tell us which app and device you are using, and the exact error message if there is one.
