<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from tools/release/public-root/README.md at commit 5fe772e9baf1fbd1be25fefcf85283d74d6a03f9 -->

<p align="center">
  <img src="/docs/user/images/fidenne-icon.png" width="128" height="128" alt="Fidenne icon">
</p>

<h1 align="center">Fidenne</h1>

<p align="center">
  A free app that sends your Mac's music to your external DAC
</p>

<p align="center">
  <b>Public beta 1 — <a href="https://github.com/fidenne/fidenne/releases/latest">Download</a> · <a href="https://fidenne.github.io/fidenne/">Install and use guide (Korean)</a></b>
</p>

<br>

<p align="center">
  <img src="/docs/user/images/fidenne-home.png" width="860" alt="Fidenne music page — now playing, today's listening, playlists, the bottom playback bar">
</p>

<br>

## What it is

An app for people who listen to Apple Music, Spotify and YouTube Music on a Mac and send the sound to an external DAC.
You keep using the player you know; before the sound reaches the DAC, Fidenne shapes it or converts it to a format your DAC handles well.

<br>

## The path your sound takes

```
Player  →  Fidenne (EQ · Ostrum · Crossfeed · output conversion)  →  your DAC
Player  →  macOS  →  your DAC                                        (PCM Direct)
```

PCM Direct means Fidenne does not process the sound; it goes through macOS straight to the DAC.
The Playback Chain in the app shows at a glance which path is in use.

<br>

## What you can do

- Choose the output mode that suits your DAC — DSD (DoP) · PCM 352.8 kHz · PCM Direct.
- Change EQ, Ostrum, Crossfeed and filters and hear the result right away.
- Search the same way in every service, and keep favourites and playlists in the Fidenne library.
- Keep a listening history on this Mac only. Sound is never recorded.

<br>

## What you need

A Mac with Apple silicon (M1 or later), macOS 26 or later, and a **wired external DAC connected directly by USB**. The app is free.

<br>

## Installation

Public beta 1 is out. Install it like this.

1. Download the `.dmg` file from the [releases page](https://github.com/fidenne/fidenne/releases/latest) of this repository.
2. Open the `.dmg` and drag Fidenne into the **Applications** folder.
3. Open Fidenne from Applications and press **Open** if a confirmation window appears.
4. Follow the first-run setup. Allow the permissions macOS asks for.

Before the first playback, turn down the volume on your DAC and amplifier. Step-by-step instructions are in the [install and use guide](/docs/user/GUIDE.md) (Korean only) and the [User manual](/docs/user/en/MANUAL.md).

<br>

## What Fidenne uses

A free app made by an individual, not affiliated with Apple, Spotify or Google.

- **Apple Music · Spotify** — Fidenne controls each app for you. Spotify's search and playlist screens work only with a Spotify developer key you create yourself, and that is optional.
- **YouTube Music** — an experimental feature connected through a browser extension. It reads only the track on the page you opened and never touches ads. What it reads goes only to Fidenne on this Mac and nowhere else.
- **Lyrics · headphone measurements · song search and charts** — public data from LRCLIB, squig.link and Apple, fetched to this Mac. Copyright stays with the rights holders and the measurers.
- **Sound** — processed only on this Mac. Never recorded or sent anywhere.
- **Album covers and lyrics** — kept on this Mac temporarily for quick display and removed 30 days after last use. Pictures from song search and charts stay in memory only.

The full list is in the [Privacy notice](/PRIVACY.en.md).

<br>

## Help

- [Install and use guide](/docs/user/GUIDE.md) (Korean only) — from installing to everyday use, in order.
- [User manual](/docs/user/en/MANUAL.md) · [Troubleshooting guide](/docs/user/en/TROUBLESHOOTING.md) · [Known limitations](/docs/user/en/KNOWN_LIMITATIONS.md)
- Contact: fidenne.support@gmail.com

## Issues

Bugs and suggestions are received as issues in this repository. For anything hard to write as an issue, use email: **fidenne.support@gmail.com**.
Please do not write security problems in a public issue; report them by the method in `SECURITY.en.md`.

When you report, attach the support file made by **Help > Create diagnostics for a problem report...** in the app (it shows its content before anything is sent) to a mail and write one line on what happened. Do not post the support file in an issue.
**Send by mail** opens your mail app; with another mail service, **Copy mail form** gives the address, subject and form to paste. The app version and macOS version are already in the form and the support file. The app sends nothing on its own.

<br>

<sub>Apple Music is a trademark of Apple Inc., Spotify of Spotify AB and YouTube Music of Google LLC. Fidenne is not affiliated with these companies.</sub>

<sub>Used under free-to-use terms — see `LICENSE`. Third-party components in the app are listed in the `THIRD_PARTY_NOTICES.md`.</sub>
