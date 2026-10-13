<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from tools/release/public-root/README.md at commit 5fe772e9baf1fbd1be25fefcf85283d74d6a03f9 -->

# Fidenne

The public repository of **Fidenne**, a music playback and sound processing app for macOS.

The app and engine are distributed as **free binaries** whose source is not published (signed and notarized). This repository holds the public parts around them —
the user manual, the privacy notice, and the releases and issues.

> **Public beta — in final review.** When the review is done, get it from the releases page of this repository; report problems by either of the two ways under "Issues" below.

## What is here

| Folder | What |
|---|---|
| `docs/user/en/` | User manual · troubleshooting guide · task-based guides · explanations of how things work |
| `PRIVACY.en.md` | Privacy notice |
| `LICENSE` | Fidenne Free Use Terms |
| `THIRD_PARTY_NOTICES.md` | Third-party component notices |

**Not here yet** — still being polished for publication: the SDK for building extensions · the list of extension ideas · the MCP server.

## What Fidenne uses

Fidenne is a free app made by an individual and is not affiliated with Apple, Spotify or Google. Apple Music is a trademark of
Apple Inc., Spotify of Spotify AB and YouTube Music of Google LLC.

- **Apple Music** — Fidenne drives the Music app with AppleScript. It reads the library list with MusicKit; for an Apple Music track you are
  playing it asks the Apple Music catalogue for the other spelling and the same song on other services and uses the answer in memory only
  (never kept). To follow each track's source rate it reads the Music app's audio log lines (not kept).
- **Spotify** — Fidenne drives the Spotify app with AppleScript. Search and playlist screens use only a Spotify developer key you create
  yourself (optional).
- **YouTube Music** — a browser extension reads the track on the open page and passes on controls such as play and pause. It never browses
  the site on its own: one press by you opens that one page. It never touches ads. Experimental.
  What the extension reads is used only for these features and passed only to the Fidenne app on this Mac — never sold, transferred, used for ads or read by people (Limited Use).
- **Lyrics** — LRCLIB (lrclib.net). Lyrics belong to their rights holders.
- **Headphone measurements** — public measurement data from squig.link, fetched to this Mac and used for correction. The data belongs to each measurer; the app shows the measurer's name and a link to the original graph.
- **Song search and charts** — Apple's public search and charts. Their pictures are not kept on this Mac.
- **Sound** — taken from macOS audio (Core Audio) and processed only on this Mac. Never recorded or sent anywhere.
- **Kept on this Mac** — album covers and lyrics, temporarily, for quick display (removed 30 days after last seen).

The full list is in [Privacy](/PRIVACY.en.md).

## Installation

**In final review.** When it is done, get the signed and notarized app from the releases page of this repository.

Requirements: a **wired USB external DAC (required)**, a Mac with Apple silicon, macOS 26 or later.

## SDK

The SDK for building extensions is planned to be published later — its license is still being decided.

## Issues

Bugs and suggestions are received as issues in this repository. For anything hard to write as an issue, use email: **fidenne.support@gmail.com**.
Please do not write security problems in a public issue; report them by the method in `SECURITY.en.md`.

When you report, attach the support file made by **Help > Create diagnostics for a problem report...** in the app (it shows its content before anything is sent) and write the app version, macOS version, DAC and output mode, and when/what you did and what you heard or saw. The app sends nothing on its own.

## Trademarks

Apple Music is a trademark of Apple Inc., Spotify is a trademark of Spotify AB, and YouTube Music is a trademark of Google LLC. Fidenne is not affiliated with these companies and is not endorsed by them.

## License

The app and the public materials in this repository are under the **Fidenne Free Use Terms** (`LICENSE`, Korean text + English translation) — you may use it free of charge,
you pass it to other people through the official release link, and you do not distribute modified copies. There is no warranty and liability is limited. The SPDX identifier at the top of each file is
`LicenseRef-Fidenne-Freeware`, and the full text is the same in `LICENSES/LicenseRef-Fidenne-Freeware.txt`. Third-party components included in the app follow their own
licenses, and the list is in `THIRD_PARTY_NOTICES.md` (the same file is also included inside the app).
