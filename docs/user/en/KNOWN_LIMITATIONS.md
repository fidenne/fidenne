<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/KNOWN_LIMITATIONS.md (0.7.0 edition) -->

# Fidenne known limitations

Fidenne is still a **beta (0.x)**. This page gathers, in one place, today's known limits, what we left out of
beta 1, what we are fixing, what we deliberately do not do, and what we are thinking about next.
For how to use the app see the [user manual](MANUAL.md); when something does not work see the
[troubleshooting guide](TROUBLESHOOTING.md).

## Known limitations

Hardware, operating system and service limits of this version.

- It opens **only on Apple silicon (M1 and later) Macs running macOS 15 or later.** It does not open on an Intel Mac even if macOS 15 or later is installed. macOS 15 was checked in a virtual machine (install, first run, each screen); listening for long on a real Mac with a DAC has not been done yet.
- **An external DAC is recommended.** The beta is built for listening through one. Fidenne processes the sound and sends it to built-in speakers · AirPods · HDMI too; macOS mixes the result through its system mixer before sending it to the device, so it is **not bit-perfect**.
- On a wired USB DAC the DSP engine runs **on a 2-channel DAC that accepts at least one of the PCM rates the engine uses (44.1 to 768 kHz).**
  A device that takes none of them (most dongles, some monitors) is marked at the end of its name with `· PCM Direct only`, and DSP and
  library playback cannot be used with it. Only listening to Apple Music or Spotify in PCM Direct works. If playback does not start after you first turn on such a device, choose PCM Direct yourself under I/O & Diagnostics › Output method.
- Fidenne processes the sound with EQ · Ostrum · crossfeed · filters and sends it to built-in speakers · the 3.5 mm jack · AirPods (Bluetooth) · HDMI · DisplayPort · AirPlay too. macOS mixes the result through its system mixer before sending it to the device, so it is **not bit-perfect**. Bit depth and dither cannot be chosen, and DSD is not sent. A Bluetooth device in call mode pauses Fidenne's processing. This path was checked with a fake device; checking on real speakers · AirPods · monitors by ear was partial.
- A 4- or 8-channel audio interface does not use the DSP engine even if it accepts the supported rates from 44.1 to 768 kHz.
- **PCM output rates (44.1 to 768 kHz) · following the source's rate family · between-songs mode · the wait when the rate changes** were checked with automatic tests and a fake device; the time a real DAC takes to lock to a new rate and what you hear were not checked. The default wait (0.25 s) may not suit every DAC, so make it longer if the first sound is cut off. The between-songs mode applies to PCM playback of local files.
- **The EQ filter calculation changed**, so an EQ with filters in the treble may sound slightly different from the earlier version (clearer at low output rates). The calculation was checked with test signals, not by ear.
- **Audio Unit plug-ins** were checked with a test plug-in, not with every plug-in on the market. There are 4 slots, and Fidenne turns off a plug-in that cannot keep up or makes odd sound. A plug-in's behavior follows its maker's terms.
- On **base M1 and M2 Macs**, the Trellis modulator at DSD256 may not keep up and the sound may break.
  If it does, use DSD128 or another modulator. This is an estimate from measurements on an M4 MacBook, not on a real M1.
- The **Trellis modulator** is heavy: if this Mac cannot finish it in time, Fidenne stops playback and recommends ‘Precise’, ‘Safe’ or CLANS (a Choose conversion method button appears with the notice). Which Macs stop was not measured on real machines.
- **Spotify**: changing lists can still let a previous list’s song through briefly at a track boundary. Version 0.7.0 narrows queue delivery to the end of a track and briefly lowers output when a leftover is detected. This mitigates the problem; it does not establish that every case is gone.
- **YouTube Music**: the cover of a song in the play queue is sometimes missing. Playback is not affected.
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
- The **YouTube Music** extension works only in Google Chrome, Microsoft Edge and Safari. Safari needs version 18.4 or later.
  The Safari extension appears in Safari only for a Fidenne opened from the **Applications folder** (or the Applications folder in your home folder); an app opened from inside the downloaded .dmg or from the Downloads folder does not show it.
  For Chrome · Edge, multiple browsers can be connected; Fidenne follows the browser where you start playback.
  If the site changes its layout, track information may be empty for a while.
- **Lyrics**: some tracks that do have lyrics show "marked as an instrumental" and no lyrics.
  You can attach them yourself with **Link lyrics file** in the lyrics panel.
- Long listening on a real DAC, unplugging and replugging the device, and playback after waking from sleep have not been checked enough yet. If something sounds wrong, please tell us.

## What macOS does not allow

Limits that come from how macOS and the music apps work, which Fidenne cannot change.

- **DoP instead of native DSD.** macOS's standard USB audio driver has no DSD format, so Fidenne uses DoP, which carries DSD inside PCM without loss. The DSD your DAC receives is the same; the difference is the top rate (up to DSD256). Your DAC must accept DoP. Native output at DSD512 and above is being considered through a network endpoint (a Linux device in front of the DAC).
- **Fidenne cannot take the music app's original data.** Apple Music and Spotify offer no official way to hand their sound to another app, so Fidenne takes the sound macOS plays and processes it. The start of a track you play for the first time may arrive after macOS changed its rate (from the next play it arrives at the original rate), and bit-perfect delivery is not guaranteed.
- **Stereo (two channels) only.** Multichannel sound such as Dolby Atmos, and 4- or 8-channel audio interfaces, cannot use the engine.
- Fidenne processes PCM sound and sends it to Bluetooth · AirPlay · HDMI too; macOS mixes the result through its system mixer before sending it to the device, so it is **not bit-perfect**. **DSD is not sent to these devices.** DSD and bit-perfect integer PCM need a wired USB DAC that takes DoP · integer PCM.
- **PCM Direct cannot match the rate track by track,** because the sound does not pass through Fidenne.
- **A DAC whose volume control is linked to the macOS volume has its DAC-side volume at maximum during DSD · integer PCM playback.** Fidenne keeps the loudness the same inside Fidenne and gives the volume back afterwards, but during playback that volume cannot go higher. Details: [DAC volume and DSD (DoP) · integer PCM](TROUBLESHOOTING.md#dac-volume-and-dsd-dop--integer-pcm)
- **Apple silicon Macs with macOS 15 or later** only.

## What is hard for an app made by one person

- **Few DACs have been tested** — only the few the developer owns. Please report anything odd on other DACs.
- **Answers and fixes can take time.** Reports come by mail and GitHub issues; a reply may not be immediate.
- **The interface comes in Korean, English and Japanese.** The English and Japanese sentences are AI-translated drafts that no native speaker has reviewed.
- **No Windows or Intel Mac versions.**
- **Versions older than macOS 15 are not supported.** The Liquid Glass screen effects and translating lyrics with Apple Intelligence need macOS 26 or later. On macOS 15 Fidenne uses the earlier surface material (the playback capsule is always opaque) and the other translation routes instead.
- **When a music service changes its pages or rules,** that connection (especially the YouTube Music extension) can stop suddenly, and a fix can take a few days.
- **Sound measurements are digital only.** There is no equipment to measure a DAC's analogue output.
- **No paid service keys inside the app,** so Spotify search and playlists need a Spotify developer key you create yourself (optional).
- **AI lyrics translation has been confirmed working with Claude (Anthropic) only.** OpenAI and Gemini follow each company's public API documentation and current model names but have not yet been tried with a real account. If 「연결 시험…」 (Test connection) shows an error, please report it with the message.

## Left out of beta 1

Things that exist in the code or are built, but are off or not shipped in beta 1.

- **A/B · ABX · Auto Bypass · Loop comparison** — hidden. It comes back after we fix both sides turning off when Ostrum is toggled during a comparison.
- **YouTube Music** — an experimental feature. A fresh install has it off; turn it on at the top of Settings → General.
  If you already used it, it stays on.
- **Playlists imported through a YouTube account connection** — not in this version. Lists imported that way earlier are not shown.
  Importing a Google Takeout file still works.
- **Receiving a single app's sound (per-app system tap)** — not in this version (whole system only).
- **The "연결 후보" (link candidates) screen for joining similar songs** — hidden. Songs that are certainly the same are still merged into one row in the listening history.
- **Finding lyrics on Chinese lyrics servers** — not in this version. Lyrics come from LRCLIB only.
- **Light theme** — not fully supported yet. The app is tuned for the dark theme, so some screens may look off in light.
- **English · Japanese UI** — included, but the translations are AI drafts that no native speaker has reviewed. There is no language switch inside the app; it follows macOS's language order. Some screens may cut off longer English · Japanese text.
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
- **DSD · PCM oversampling** — with EQ · Ostrum · Crossfeed off, nothing changes the tone.
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

- **Planned** — small details fixed right after release (alignment, filling the empty space on the music home, wider YouTube Music search).
- **Planned** — a global "follow the source" switch for filters, dither for every modulator.
- **Planned** — a Spotify queue playlist; the same home screen for the local library as for services.
- **Under consideration** — rolling back to the previous version if an update fails; making diagnostic files smaller.
- **Planned** — changing filters and modulators within DSD without a gap.
- **Planned** — EQ · Ostrum · crossfeed on USB dongles that cannot take any supported PCM rate from 44.1 to 768 kHz.
- **Under consideration** — UI languages beyond English and Japanese, and a native-speaker review of the English and Japanese translations.
- **Under consideration** — one-click sound setups per headphone; sharing the current sound path as an image.
- **After the official release** — an SDK that lets other developers add features to Fidenne, published once the app is judged stable and complete after the official release.
- **Under consideration** — moving tracks between services (Spotify · YouTube Music tracks into the Apple Music library).
- **Under consideration** — enriching the library with album notes, credits and artist information (file tags stay untouched; added from a public music database).
- **Under consideration** — grouping an untidy music folder into albums · artists · covers automatically; syncing untimed lyrics by hand.
- **Under consideration** — bringing back A/B · ABX, a remote control, home theatre (multichannel HDMI).
