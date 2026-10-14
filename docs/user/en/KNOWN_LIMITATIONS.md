<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/KNOWN_LIMITATIONS.md at commit bcfecdb9 -->

# Fidenne known limitations

Fidenne is still a **beta (0.x)**. This page gathers, in one place, today's known limits, what we left out of
beta 1, what we are fixing, what we deliberately do not do, and what we are thinking about next.
For how to use the app see the [user manual](MANUAL.md); when something does not work see the
[troubleshooting guide](TROUBLESHOOTING.md).

## Known limitations

Hardware, operating system and service limits of this version.

- It opens **only on Apple silicon (M1 and later) Macs running macOS 26 or later.** It does not open on an Intel Mac even if macOS 26 is installed.
- **A wired USB external DAC is required.** The beta is built for listening through one.
- The DSP engine runs **only on a 2-channel external DAC that accepts 352.8 kHz or higher.** Built-in speakers,
  AirPods, most dongles and monitors do not meet this; they are marked at the end of their name, and DSP and
  library playback cannot be used with them. Only listening to Apple Music or Spotify in PCM Direct works.
- A 4- or 8-channel audio interface does not use the DSP engine even if it accepts 352.8 kHz.
- On **base M1 and M2 Macs**, the Trellis modulator at DSD256 may not keep up and the sound may break.
  If it does, use DSD128 or another modulator. This is an estimate from measurements on an M4 MacBook, not on a real M1.
- DSD in the 48 kHz family is not opened.
- Screens are tuned for the **default 100% interface scale**. At 75, 125 and 150% some screens are less polished. 100% is what development is measured against; please report a screen that breaks at another scale and we will fix it.
- System audio is received as the **whole system** only. Picking a single app to receive is not in this version.
- The beta was tested mainly on the maker's one Mac and three external DACs.
  If something is wrong on another DAC, a Bluetooth device or an HDMI output, please tell us.
- The longer a linear-phase filter is, the longer the delay before the sound comes out. Enlarging the buffer does not shorten it.
- The delay shown on screen is an estimate made inside the app. It does not include the time from macOS, the DAC or the speaker to your ear.
- Receiving sound needs macOS permissions (system audio, microphone, automation).
  If you deny one, or turn it off later, the features that need it (receiving sound, track information, playback control) stop.
- Following each **Apple Music** track's sample rate reads the playback record the Music app leaves behind.
  If it cannot be read, the app follows only the track information it polls about once a second, and switches may come late.
  On a non-administrator standard account macOS may block it (still being confirmed).
- **Spotify** depends on the network and your login state. If your login expires or a permission is denied, you may have to handle the macOS authorization window yourself.
- The **YouTube Music** extension works only in Google Chrome and Microsoft Edge.
  Install it in **only one** of them; with both, a tab may open in the browser you do not usually use.
  If the site changes its layout, track information may be empty for a while.
- **Lyrics**: some tracks that do have lyrics show "marked as an instrumental" and no lyrics.
  You can attach them yourself with **Link lyrics file** in the lyrics panel.
- Long listening on a real DAC, unplugging and replugging the device, and playback after waking from sleep have not been checked enough yet. If something sounds wrong, please tell us.

## What macOS does not allow

Limits that come from how macOS and the music apps work, which Fidenne cannot change.

- **DoP instead of native DSD.** macOS's standard USB audio driver has no DSD format, so Fidenne uses DoP, which carries DSD inside PCM without loss. The DSD your DAC receives is the same; the difference is the top rate (up to DSD256). Your DAC must accept DoP. Native output at DSD512 and above is being considered through a network endpoint (a Linux device in front of the DAC).
- **Fidenne cannot take the music app's original data.** Apple Music and Spotify offer no official way to hand their sound to another app, so Fidenne takes the sound macOS plays and processes it. The start of a track you play for the first time may arrive after macOS changed its rate (from the next play it arrives at the original rate), and bit-perfect delivery is not guaranteed.
- **Stereo (two channels) only.** Multichannel sound such as Dolby Atmos, and 4- or 8-channel audio interfaces, cannot use the engine.
- **The engine cannot output over Bluetooth, AirPlay or HDMI.** Engine output needs a wired USB DAC that accepts 352.8 kHz.
- **PCM Direct cannot match the rate track by track,** because the sound does not pass through Fidenne.
- **A DAC whose volume control is linked to the macOS volume has its DAC-side volume at maximum during DSD · integer PCM playback.** Fidenne keeps the loudness the same inside Fidenne and gives the volume back afterwards, but during playback that volume cannot go higher. Details: [DAC volume and DSD (DoP) · integer PCM](TROUBLESHOOTING.md#dac-volume-and-dsd-dop--integer-pcm)
- **Apple silicon Macs with macOS 26 or later** only.

## What is hard for an app made by one person

- **Few DACs have been tested** — only the few the developer owns. Please report anything odd on other DACs.
- **Answers and fixes can take time.** Reports come by mail and GitHub issues; a reply may not be immediate.
- **The interface is Korean only for now.** An English interface comes later.
- **No Windows or Intel Mac versions.**
- **Older macOS versions are planned after testing.** Today it needs macOS 26 or later. Versions that have the features Fidenne relies on — such as taking another app's sound, available since macOS 14.2 — will be tested one by one and added as they pass.
- **When a music service changes its pages or rules,** that connection (especially the YouTube Music extension) can stop suddenly, and a fix can take a few days.
- **Sound measurements are digital only.** There is no equipment to measure a DAC's analogue output.
- **No paid service keys inside the app,** so Spotify search and playlists need a Spotify developer key you create yourself (optional).

## Left out of beta 1

Things that exist in the code or are built, but are off or not shipped in beta 1.

- **A/B · ABX · Auto Bypass · Loop comparison** — hidden. It comes back after we fix both sides turning off when Ostrum is toggled during a comparison.
- **Convolution (applying an IR)** — hidden. Changing the IR can make the sound jump loudly for an instant; it stays off until that is fixed.
- **YouTube Music** — an experimental feature. A fresh install has it off; turn it on at the top of Settings → General.
  If you already used it, it stays on.
- **Playlists imported through a YouTube account connection** — not in this version. Lists imported that way earlier are not shown.
  Importing a Google Takeout file still works.
- **Receiving a single app's sound (per-app system tap)** — not in this version (whole system only).
- **The "연결 후보" (link candidates) screen for joining similar songs** — hidden. Songs that are certainly the same are still merged into one row in the listening history.
- **Finding lyrics on Chinese lyrics servers** — not in this version. Lyrics come from LRCLIB only.
- **Light theme** — not fully supported yet. The app is tuned for the dark theme, so some screens may look off in light.
- **YouTube Music list screen** — still differs from the Apple Music and Spotify playlist screen (no large cover or sort; just name, song count and ▶ ⤨). The first update gives it the same screen.
- **English UI** — not yet. Sentences are Korean; only DSP page terms are English.
- **Developer tools** — not in this version.
- **Chain presets** — not yet. The crossfeed head model and SOFA HRTF are plans only.

## Being fixed

Symptoms you may meet. We have no reliable workaround to offer yet.

- **EQ · Ostrum is barely audible** — the case where EQ vanished after relaunch and two causes for Ostrum are fixed.
  If it is still inaudible, tell us with a diagnostic export. We have not fixed everything yet.
- **Playing after stopping with a FIR filter and a +24 dB shelf in EQ gives silence** — not fixed yet. Please test with the volume low.
- **While Spotify plays, the engine input looks silent** — only in some environments. Not fixed yet.
- **The input spectrum freezes during playback** — only in some environments. Not fixed yet.
- **Starting a track across services can break the sound once, 1–4 seconds in** — the track's rate changes and the engine restarts.
- **Tapping a track in Apple Music seems to play a different track briefly first** — not fixed yet.
- **Sound from a browser (Edge) is labelled as the Spotify track played just before** — a labelling problem.
- **Spotify repeat and the next-up list** — the repeat display can disagree with the Spotify app, and the next track may not show at the end of the list.
- **On some DACs integer PCM (24 · 16-bit) output is refused, or PCM Direct waits for a connection** — we are confirming the fix on a real DAC.
- **Crossfeed sounds different from day to day** — one cause is fixed. Tell us if there is more.
- **The narrow album mode is slightly asymmetric left to right** — no effect on the sound.

## What we do not do

Deliberately not done.

- **We never store the sound or send it out.** There is no recording feature.
- **PCM Direct** — Fidenne does not process the sound. It goes player app → macOS → DAC.
  The sample rate is not matched track by track (because the sound does not pass through Fidenne, it cannot change the output rate to the track's (input) rate): when the DAC's rate and the track's differ, macOS converts.
  The DAC's rate is set once at start (44.1 kHz for Spotify; the track's rate or 44.1 kHz when the DAC sits at a rate that is not ordinary PCM, such as DSD or 352.8 kHz).
  macOS sits in the middle, so we do not claim "bit-perfect".
- **DSD · PCM 352.8 kHz** — with EQ · Ostrum · Crossfeed off, nothing changes the tone.
  But the conversion each format needs (upsampling filter · DSD modulator · dither · headroom) is applied,
  and the chosen filter and modulator can change the character of the sound.
- We **do not touch YouTube ads.**
- We **do not browse a site on our own.** Only the screens you opened yourself are read.
- We **do not replace or circumvent** a music service subscription. We do not break DRM. Tracks play through each service's app and your own account.
- **No account or analytics is required.** There are no ads.
- Answers from the Apple catalogue are **not stored.** They are used on the spot.
- Information Spotify provides is not used for cross-service track linking, listening statistics or sending to other services.
- No dynamic EQ.

## What comes next

No dates are promised. The order may change after beta feedback.

- **Planned** — small details fixed right after release (alignment, click-to-sort list headers, filling the empty space on the music home, wider YouTube Music search, YouTube Music lists on the same playlist screen as the other services).
- **Planned** — a global "follow the source" switch for filters, dither for every modulator, a 7th-order CLANS modulator option.
- **Planned** — a Spotify queue playlist; the same home screen for the local library as for services.
- **Under consideration** — rolling back to the previous version if an update fails; making diagnostic files smaller.
- **Under consideration** — other UI languages such as English.
- **Under consideration** — moving tracks between services (Spotify · YouTube Music tracks into the Apple Music library).
- **Under consideration** — enriching the library with album notes, credits and artist information (file tags stay untouched; added from a public music database).
- **Under consideration** — grouping an untidy music folder into albums · artists · covers automatically; syncing untimed lyrics by hand.
- **Under consideration** — bringing back A/B · ABX and convolution, wider PCM upsample rates, a remote control, home theatre (multichannel HDMI).
