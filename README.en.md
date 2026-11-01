<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from tools/release/public-root/README.md at commit 5fe772e9baf1fbd1be25fefcf85283d74d6a03f9 -->

<p align="center">
  <img src="/docs/user/images/fidenne-icon.png" width="128" height="128" alt="Fidenne icon">
</p>

<h1 align="center">Fidenne</h1>

<p align="center">
  A Mac app that refines the sound of the music app you already use with DSP and sends it to your external DAC
</p>

<p align="center">
  <b>Public beta 1 · 0.7.0 — <a href="https://github.com/fidenne/fidenne/releases/latest">Download</a> · <a href="https://fidenne.github.io/fidenne/">Install and use guide (Korean)</a></b>
</p>

<br>

<p align="center">
  <img src="/docs/user/images/fidenne-home.png" width="860" alt="Fidenne music page — now playing, today's listening, playlists, the bottom playback bar">
</p>

<br>

## What it is

Fidenne is a Mac app that refines the sound of the music app you already use with DSP and sends it to your external DAC.
Keep using Apple Music, Spotify, YouTube Music or the app you know, and choose DSP and an output mode suited to your DAC in Fidenne.
The music still plays in each service's own app, so play counts and ads stay with the service; Fidenne never blocks or skips ads.

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

- Choose the output mode that suits your DAC — DSD (DoP) · PCM oversampling (44.1 to 768 kHz) · PCM Direct.
- Change EQ, Ostrum, Crossfeed and filters and hear the result right away.
- Check the path your sound takes and the processing in use in Playback Chain.
- Control the service app you already use from Fidenne and view track information and lyrics alongside it (playback stays in each service’s own app).
- Sound is never recorded.

<br>

## What's new in 0.7.0

**Sound**
- Choose the PCM output rate from supported rates in the 44.1 and 48 kHz families (44.1 to 768 kHz). With **Follow the source's rate family** on, a 44.1 kHz-family song goes out in the 44.1 family and a 48 kHz-family song in the 48 family; **Auto (highest the device takes)** picks the highest multiple your DAC accepts.
- Choose whether songs join **Unchanged** or **Smooth**, and set per DAC how long to wait when the rate changes.
- Fidenne processes the sound with EQ, Ostrum, crossfeed and filters and sends it to built-in speakers, the 3.5 mm jack, AirPods (Bluetooth) and HDMI too. macOS mixes the result through its system mixer before sending it to the device, so it is not bit-perfect; the screen shows **not bit-perfect**.
- **The sound changes** — the EQ filter coefficients are now computed to match their analog prototypes. At high frequencies (especially above 16 kHz) the curve you set follows the real curve more closely, so an EQ with filters in the treble can sound slightly different with the same settings. The difference is larger at low output rates.
- **CLANS** is a new experimental conversion method in 0.7.0, available at DSD128 and DSD256.
- If this Mac cannot finish the Trellis conversion in time, playback stops and Fidenne recommends **Precise · Safe · CLANS** with a **Choose conversion method** button. An AU plug-in that runs late or stalls is switched off by Fidenne and the sound carries on.
- The long-tap filters gain **Cardinal Sinc 128K and 64K**, each with a **Follow** twin that follows the song's rate.
- On the **Plug-in** page, put up to 4 Audio Unit effect plug-ins in the path the sound takes.
- The Convolution (IR) page is available starting with this release.

**Screens and tools**
- On the home page, drag songs into a playlist, group songs of the same day, and **Remove from History** the entries you do not want to see.
- Import an EQ from Room EQ Wizard (REW), Equalizer APO or AutoEq text files.
- Call play, next, previous, the current song, bypass of sound processing and an EQ preset from the Shortcuts app.
- Lyrics get a **pronunciation** line, and you can reorder the original, pronunciation and translation lines.
- The screens can be used in English and Japanese (they follow the language order set in macOS). The translations are AI drafts that no native speaker has reviewed yet.
- When something sounds odd, press **⌥⌃⌘K** (Help › Mark That Something Was Off) to mark that moment in the diagnostic record, so it is easy to find in a problem report. The record stays on this Mac.
- If a YouTube Music tab starts by itself while you listen to another service, your song is left as it is. In Apple Music and Spotify, Previous goes back to the start of the song when you have heard more than 3 seconds.
- Song lists behave the Mac way (one click selects, double-click or Return plays). The Playback menu gains volume and mute and a **Sleep Timer**, and lyrics gain restoring a **Previous Translation**.

The full list of changes is on the [releases page](https://github.com/fidenne/fidenne/releases/latest).

<br>

## What you need

- A Mac with Apple silicon (M1 or later) and **macOS 15 or later**. It does not open on an Intel Mac.
- An **external DAC is recommended.** With a wired DAC connected directly by USB, Fidenne takes hold of the device itself and sends it the processed sound. DSP (EQ · Ostrum · Crossfeed) and DSD · PCM output run on a **2-channel DAC that accepts at least one of the PCM rates the engine uses (44.1 to 768 kHz)**. DSD needs a DAC that can unpack DoP.
- Fidenne sends processed sound to built-in speakers, the 3.5 mm jack, AirPods and HDMI too. macOS mixes the sound once more before sending it to these devices, so the screen shows **not bit-perfect**. Devices that are not 2-channel, such as 4- and 8-channel audio interfaces, or accept none of the supported rates from 44.1 to 768 kHz use **PCM Direct**, without Fidenne processing.
- The app is free.

<br>

## Installation

This is 0.7.0 of public beta 1. Install it like this.

1. Download the `.dmg` file from the [releases page](https://github.com/fidenne/fidenne/releases/latest) of this repository.
2. Open the `.dmg` and drag Fidenne into the **Applications** folder. Do not run it straight from the disk image or the Downloads folder (the Safari extension would not show).
3. Open Fidenne from Applications and press **Open** if a confirmation window appears.
4. Follow the first-run setup. Allow the permissions macOS asks for.

Before the first playback, turn down the volume on your DAC and amplifier. Step-by-step instructions are in the [install and use guide](/docs/user/GUIDE.md) (Korean only) and the [User manual](/docs/user/en/MANUAL.md).

<br>

## What Fidenne uses

A free app made by an individual, not affiliated with Apple, Spotify or Google.

- **Apple Music · Spotify** — Fidenne controls each app for you. Spotify's search and playlist screens work only with a Spotify Premium account and a Spotify developer key you create yourself, and that is optional. Every Spotify item there opens in Spotify through **OPEN SPOTIFY**. Without connecting, Fidenne still processes the sound of the Spotify app.
- **YouTube Music** — an experimental feature connected through a browser extension. It reads only the track on the page you opened and never touches ads. What it reads goes only to Fidenne on this Mac and nowhere else.
- **Lyrics · headphone measurements · song search and charts** — public data from LRCLIB, squig.link and Apple, fetched to this Mac. Copyright stays with the rights holders and the measurers.
- **Sound** — processed only on this Mac. Never recorded or sent anywhere.
- **Album covers and lyrics** — ordinary artwork and the lyrics lookup cache expire thirty days after last use. Spotify artwork expires thirty days after receipt. Lyrics and translations saved in the Lyrics tab stay until you delete them. Search and chart pictures stay in memory only.

The full list is in the [Privacy notice](/PRIVACY.en.md).

**How the browser extension uses information (Limited Use)** — Information received by the Fidenne extensions for Safari, Chrome and Edge is used only to tell Fidenne on this Mac what is playing now and pass the commands you press to the YouTube Music page. It is not sold, used for advertising, or passed to anyone else. The Safari extension is included in the Fidenne app. The Chrome extension’s use of information follows the Chrome Web Store User Data Policy, including the Limited Use requirements.

<br>

## Help

- [Install and use guide](/docs/user/GUIDE.md) (Korean only) — from installing to everyday use, in order.
- [User manual](/docs/user/en/MANUAL.md) · [Troubleshooting guide](/docs/user/en/TROUBLESHOOTING.md) · [Known limitations](/docs/user/en/KNOWN_LIMITATIONS.md)
- Contact: fidenne.support@gmail.com
- Rights and terms enquiries: fidenne.support+legal@gmail.com

## FAQ

**Is the source code public?**
No. Fidenne is a personal project, and the app's source code is not published. The app stays free.

**Is there an SDK for building extensions?**
One is planned, but it is not confirmed and there is no date yet. The licence under consideration is Apache-2.0. Details will follow when it is published.

## Issues

Bugs and suggestions are received as issues in this repository. For anything hard to write as an issue, use email: **fidenne.support@gmail.com**.
Please do not write security problems in a public issue; report them by the method in `SECURITY.en.md`.

When you report, attach the support file made by **Help > Create diagnostics for a problem report...** in the app (it shows its content before anything is sent) to a mail and write one line on what happened. Do not post the support file in an issue.
**Send by mail** opens your mail app; with another mail service, **Copy mail form** gives the address, subject and form to paste. The app version and macOS version are already in the form and the support file. The app sends nothing on its own.

<br>

<sub>Apple Music is a trademark of Apple Inc., Spotify of Spotify AB and YouTube Music of Google LLC. Fidenne is not affiliated with these companies.</sub>

<sub>Used under free-to-use terms — see `LICENSE`. Third-party components in the app are listed in the `THIRD_PARTY_NOTICES.md`.</sub>
