<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/GUIDE.md -->

# Fidenne Installation & User Guide — Step by Step

[한국어](../GUIDE.md) | English | [日本語](../ja/GUIDE.md)

Fidenne is an app that refines the sound from music apps on your Mac (Apple Music · Spotify · YouTube Music) and sends it to your DAC.
A DAC is a small device (an external USB device) that converts digital audio to analog and sends it to your headphones or speakers.

This guide walks you through everything step by step, from installation to everyday use. Each step explains what you will see, what to click, and what to do if you get stuck. Follow the links at each step if you need more detail.

- Part 1 **Install (설치)**: 12 steps. From downloading to hearing sound for the first time.
- Part 2 **Using Fidenne**: 10 steps. How to use the app.
- To browse by screen layout, see the [User Manual](MANUAL.md); to browse by task, see the [How-To Guide](HOW-TO.md); if something goes wrong, see the [Troubleshooting Guide](TROUBLESHOOTING.md).

---

# Part 1. Install

## Install 1 · Start

Fidenne refines the sound produced by music apps and sends it to your DAC. Sound travels in the order **Playback App → Fidenne → DAC**.
You pick and play music as usual in the Apple Music · Spotify · YouTube Music app (or browser), and Fidenne receives the audio in between, processes it, and passes it to your DAC.
Fidenne does not save audio or write it to files.

Installation takes eight steps. Those steps (preparation · download · move · first open · first-time setup · permissions · volume · when stuck) are covered one by one from Install 2 to 9, followed by three optional connections (two for Spotify, one for YouTube Music).

More: [User Manual — At a Glance](MANUAL.md#0-at-a-glance)

## Install 2 · Requirements

Fidenne opens only on an **Apple silicon Mac** (M1 chip or later) running **macOS 15 or later**. You can check which chip your Mac has from the Apple logo in the top menu bar › **About This Mac**.
The chip name should start with "Apple M". If macOS is older than 15, the app will not open, so run Software Update in System Settings first.

**An external DAC is recommended.** The beta was built assuming you listen through an external DAC. On a DAC connected directly via USB, the sound-refining features (such as EQ) run on 2-channel DACs that accept at least one of the PCM rates the engine uses (44.1 – 768 kHz).
Fidenne also processes sound with EQ · Ostrum · Crossfeed · filters and sends it to built-in speakers · 3.5 mm jack · AirPods · HDMI. At the end, macOS mixes it through the system mixer, so it is not bit-perfect (**via system mixer · not bit-perfect**). Devices that do not accept any of the 44.1 – 768 kHz supported rates (such as most dongles) only output via PCM Direct, which plays the audio untouched.

More: [User Manual — At a Glance](MANUAL.md#0-at-a-glance) · [Known Limitations](KNOWN_LIMITATIONS.md)

## Install 3 · Download

Download the installer from the **Releases** section on Fidenne’s public page (GitHub): `github.com/fidenne/fidenne/releases`. Open the latest release at the top and click the file ending in `.dmg`.
A `.dmg` is a disk image file used on Mac to package and distribute apps. Downloaded files usually go to your **Downloads** folder.

If the download takes a while, wait until it finishes. If the file does not open or has a different name, check again that you picked the latest release.
The app is signed and notarized before distribution. Do not use files downloaded from anywhere else.

More: [How-To Guide — Getting the Beta and Reporting Issues](HOW-TO.md#30-get-the-beta-and-report-a-problem)

## Install 4 · Move

Double-click the downloaded `.dmg` to open a small window. Drag the **Fidenne** icon inside the window onto the **Applications** folder.
Once copying finishes, close the window; you can also eject (⏏) the mounted disk image from the Finder sidebar.

Keeping the app in the Applications folder makes future updates easier, and the Safari extension for YouTube Music only appears in Safari when the app is opened from that folder. Do not open it directly from inside the downloaded `.dmg`. If a prompt says an app with the same name already exists, choose to replace it with the new one.

## Install 5 · First Open

Open Fidenne from the Applications folder. For apps downloaded from the internet, macOS asks once, "Are you sure you want to open it?" Click **Open (열기)**.

If it still does not open, you can allow Fidenne in System Settings › Privacy & Security. The exact wording in this window may vary slightly depending on your macOS version.
If your Mac is running a version older than macOS 15, the app will not open at all. In that case, go back to Install 2 and update macOS.

More: [Troubleshooting Guide — Other Symptoms](TROUBLESHOOTING.md#8-other-symptoms)

## Install 6 · Fidenne First-Time Setup

The first time you open the app, the "Fidenne First-Time Setup" window appears and walks you through five steps (shown as `1 / 5` at the top of the window). Move between steps using **Back / Next**.

1. **The DAC your sound goes to (소리가 나갈 DAC)**: Select your DAC. If you are not sure, you can click **Choose later (나중에 고르기)**. If your DAC does not appear, plug it in and refresh.
2. **How sound is captured (소리를 가져오는 방법)**: **Fidenne Inlet** is selected by default. It is a virtual device that captures audio from music apps in its original state. You can leave it as is.
   If it is not installed yet, click **Install… (설치…)**. macOS will ask for your administrator password once, and all sound will pause briefly during installation.
   Virtual audio devices like Inlet are installed separately because macOS only loads them from a system folder. If you prefer not to install it, choose **System tap (시스템 탭)** (requires no installation, but captures at 48 kHz).
3. **What macOS will ask (macOS가 물어볼 것들)**: Nothing is asked right now; macOS will ask when you first use each feature.
4. **What Fidenne Does and Doesn’t Do (Fidenne이 하는 것 · 하지 않는 것)**: A summary of what Fidenne does and does not do. Read it and click **Next (다음)**.
5. **Licence and internet access (라이선스와 인터넷 연결)**: Below the terms are four checkboxes (**Agree to All (전체 동의)** · **[Required] Terms of Use** · **[Optional] Use features that connect to the internet ([선택] 인터넷 연결 기능 사용)** · **[Optional] Diagnostic records for problem reports ([선택] 문제 제보용 진단 기록)**). The optional checkboxes are off by default, and you must check the required box before you can click **Start (시작)**. If you do not agree and click Quit, the app closes. Playback still works even if you leave the optional boxes unchecked.

Once you finish all five steps, the sidebar (page list) and main page appear in the same window. This setup window will not appear again on future launches.
You can change the optional consents later in Settings. If you do not agree to internet access, online features remain turned off.

More: [User Manual — First Launch](MANUAL.md#1-first-launch--the-five-step-first-run-setup)

## Install 7 · Permissions

macOS asks for permissions the moment you first use a feature that needs them. You may see the following four prompts:

- **Audio Recording · System Audio**: When capturing sound from other apps. Even though the prompt says "Recording", Fidenne does not save audio.
- **Microphone (마이크)**: When capturing sound through an input device such as Fidenne Inlet. This also does not save audio or send it anywhere.
- **Automation**: When reading the current track info from Apple Music or Spotify and sending play/pause commands.
- **Apple Music Library**: When reading your library via MusicKit.

Click **Allow (허용)** when prompted. If you declined by mistake, turn Fidenne back on for that item in System Settings › Privacy & Security.
If you use the app without granting these permissions, sound may not come through or track info may not appear.

More: [User Manual — First Launch](MANUAL.md#1-first-launch--the-five-step-first-run-setup) · [Troubleshooting Guide — No Sound](TROUBLESHOOTING.md#1-no-sound)

## Install 8 · Turn Down Volume Before First Playback

When you launch the app and press Play for the first time, the "Turn the volume down before starting" dialog appears before any sound plays. Turn the volume on your DAC or amplifier down to **0 or very low**.
Then click **I turned it down, start (낮췄어요, 시작)**, and slowly raise the volume while listening. Clicking **Cancel (취소)** starts nothing.

This prompt appears once on the first playback each time you launch the app. It also appears once more the first time you use a DAC with this app. This protects your ears and equipment in case the initial output is unexpectedly loud.
If nothing happens when you press Play, check whether this dialog is behind another window.

More: [How-To Guide — Turning the Volume Prompt On and Off](HOW-TO.md#24-volume-notice-before-sound-starts--turning-output-monitoring-on-and-off)

## Install 9 · When Stuck

If there is no sound or something seems wrong, first look up your symptom in the [Troubleshooting Guide](TROUBLESHOOTING.md). The most common issue, "No sound", is the very first item.

If that does not solve it, create a support file from the app’s Diagnostics menu › **Export Diagnostics for Support… (지원용 진단 내보내기…)**. Before exporting, the app shows you what is inside the file.
The app never sends anything on its own, so you decide whether to send it. Send inquiries by email to **fidenne.support@gmail.com**.
If you have a GitHub account, you can post at `github.com/fidenne/fidenne/issues`, but **only send diagnostic files by email**—never upload them to an issue.

More: [User Manual — Sending Support Files](MANUAL.md#10-sending-a-support-file) · [Troubleshooting Guide — If It Still Doesn’t Work](TROUBLESHOOTING.md#9-if-that-still-does-not-work--what-to-collect-and-send)

## Install 10 · (Optional) Connect Spotify ① Create Your App

This part is **optional**. If you pick tracks in the Spotify app, Fidenne still refines the sound and shows the current track even without a key.
You only need this if you want to use Spotify search, playlists, and playback controls inside Fidenne. Because Fidenne does not bundle a Spotify key, it uses a key from your own Spotify developer app. Sign in with your usual Spotify account.

1. Open `developer.spotify.com` in your browser and click **Log in**. You can also open it from the dots next to Spotify on Fidenne’s Streaming page › **Open Developer Dashboard (개발자 대시보드 열기)**.
2. After signing in, click your account name button and choose **Dashboard** from the menu.
3. On the **Dashboard** screen, click **Create app**.
4. Enter anything for **App name** and **App description**. In **Redirect URIs**, paste the address shown in Fidenne, `http://127.0.0.1:53682/callback` (using Fidenne’s **Copy (복사)** button), and click **Add**. Under **Which API/SDKs are you planning to use?**, check **Web API**. Leave the Website field blank.
5. Check the terms agreement box (**I understand and agree with Spotify's Developer Terms of Service and Design Guidelines**) and click **Save (저장)**.

What you agree to here are Spotify’s developer terms. You accept them directly, and those terms are set by Spotify. Button labels and layout on the website may change.

More: [How-To Guide — Connecting Spotify for the First Time](HOW-TO.md#29-connect-spotify-for-the-first-time-your-own-key) · [User Manual — Streaming Page](MANUAL.md#3-streaming-page)

## Install 11 · (Optional) Connect Spotify ② Enter Your Key

Paste the **Client ID** of the app you created into Fidenne’s field. **You only need the Client ID.** The dashboard also shows a **Client Secret**, which Fidenne does not use and has no field for. Treat it like a password and never share it with anyone. Even if you paste the full dashboard URL, Fidenne reads the ID inside it.

6. After saving, the **Basic Information** screen for your app opens. Click the copy button at the end of the **Client ID** field.
7. Paste it into the Spotify connection field on Fidenne’s Streaming page and click **Check Key (키 확인)** to verify the format. If it flags the length or invalid characters, check whether extra spaces were copied at the start or end. Once it passes, click **Connect Spotify (Spotify 연결)**.
8. A Spotify consent screen opens in your browser. Confirm your app name and click **Agree (동의)**.
9. When you see "Spotify’s authorization reply was received. Return to Fidenne to see the result.", the connection is complete. Close that tab and return to Fidenne.

Controlling playback (play, pause, skip) in Spotify requires **Spotify Premium**.
If you make too many requests, Spotify asks you to wait briefly. Your connection remains intact; just try again after the indicated time.
Once connected, **Renew Playback Permission (재생 권한 갱신)** and **Disconnect (연결 해제)** appear in the connection window.

More: [How-To Guide — Connecting Spotify for the First Time](HOW-TO.md#29-connect-spotify-for-the-first-time-your-own-key)

## Install 12 · (Optional) YouTube Music

YouTube Music is an **experimental feature**, so it is turned off initially. On a fresh install it starts off, and you enable it with the top switch in **Settings › General**.
Because YouTube Music has no Mac app, you listen in **Safari · Chrome · Edge**, and Fidenne uses an extension (a small add-on in your browser) to receive track info and control playback. Sound is captured as usual by Fidenne Inlet. If you connect multiple browsers, Fidenne follows the browser where you directly start playback. The Safari extension is bundled inside the Fidenne app, so there is no file to install—follow **Enable in Safari** below.

1. Turn on YouTube Music using the top switch in **Settings › General**.
2. Turn on **Settings › Privacy › Connect to browser extension (Safari · Chrome · Edge) (브라우저 확장과 연결 (Safari · Chrome · Edge))**.
3. Click **Installation Guide… (설치 안내…)** in the same section to open the extension setup window. Leave this window open as you follow the steps below.

**Install the extension in Chrome**

1. Enter `chrome://extensions` in Chrome’s address bar and press Return (or use **Copy Address (주소 복사)** in the setup window). Turn on the **Developer mode** switch to reveal three buttons.
2. Click **Load unpacked**. A folder picker opens.
3. In that picker, press ⌘⇧G, paste the path copied with **Copy Path (경로 복사)** in the setup window, and press Return.
4. Confirm that the folder name changes to **Chrome**, then click **Select (선택)**.
5. When **Fidenne for YouTube Music** appears in the extensions list, installation is complete. The version number may differ.
6. Refresh any open YouTube Music tabs (⌘R).

**Install the extension in Edge** — The steps are the same as Chrome; only the labels differ.

1. Enter `edge://extensions` in Edge’s address bar and press Return.
2. Turn on the **Developer mode** switch at the bottom of the sidebar.
3. Click **Load unpacked**, press ⌘⇧G in the dialog, paste the path copied with **Copy Path (경로 복사)**, press Return, and click **Select (선택)**.
4. When **Fidenne for YouTube Music** appears under other sources, you are done. Refresh any open YouTube Music tabs (⌘R).

**You can leave the Autoplay switch on the YouTube Music page either on or off.** While playing a Fidenne queue, Fidenne remembers the original state and temporarily turns the switch off when needed so tracks play through your list in order. When queue control ends or the app disconnects from the extension, it restores the original state. Any change you make manually in the meantime is not overwritten. To keep listening with tracks picked by YouTube Music after the end of your list, turn on both Fidenne’s **When the current list ends, continue with YouTube Music autoplay (현재 재생 목록이 끝나면 YouTube Music 자동 재생으로 이어 듣기)** and Autoplay on the page.

**Enable in Safari** — Do this after turning on YouTube Music in step 1 above. The Chrome/Edge connection switch in step 2 is not needed for Safari. Safari 18.4 or later is required.

1. Make sure Fidenne was opened from the **Applications** folder. If the app was opened from Downloads or inside the `.dmg`, **Settings › Privacy › YouTube Music** displays `The Safari extension appears in Safari only after you move Fidenne to the Applications folder and open it again.` Quit Fidenne, move it to the Applications folder, and reopen it from there.
2. Click **Open Safari Settings (Safari 설정 열기)** in the same section. When Safari’s Extensions settings open, enable Fidenne’s YouTube Music extension. If only Safari opens, enable it in Safari › Settings › **Extensions**.
3. Open `music.youtube.com`, click the Fidenne icon in the extension bar next to the address bar, and allow it on this website (**Always Allow**). Refresh that tab (⌘R).

**Keep tabs from sleeping** — If your browser puts inactive tabs to sleep, YouTube Music cannot respond. In Chrome, add `music.youtube.com` under Settings → Performance → Memory Saver → **Always keep these sites active**; in Edge, add it under Settings → System and performance → Optimize Performance → **Never put these sites to sleep**.

**Import playlists** — Opening a playlist page in YouTube Music while the extension is connected automatically captures it. Alternatively, import a Google Takeout (Download your data) file. Captured playlists are collected under **Streaming › YouTube Music › My Playlists**.

In Chrome and Edge, the connection is active when the bottom line of the setup window changes to **1 browser connected**. Since it is not in the web store yet, it can only be installed in Developer mode. In Safari, it is connected when playing a track on `music.youtube.com` shows that track in the bottom bar. After updating the app, click refresh (↻, or **Reload** in Edge) once on the Fidenne extension on your browser’s extensions page.
If the YouTube Music page layout changes, this may stop working. That is what "experimental feature" means.

More: [User Manual — Using YouTube Music](MANUAL.md#81-using-youtube-music-chrome-extension) · [How-To Guide — Controlling YouTube Music](HOW-TO.md#25-see-and-control-youtube-music-chrome-from-fidenne) · [User Manual — Importing Playlists](MANUAL.md#41-importing-youtube-music-playlists)

---

# Part 2. Using Fidenne

## Use 1 · Start

Once installed, these ten steps are all you need. Follow three stages: pick a device → connect a service → play.
This guide uses the English interface names. Keyboard shortcuts (such as ⌘1, ⌘4, ⌘5, where ⌘ is the Command key on your keyboard) jump straight to sidebar pages.

More: [User Manual](MANUAL.md) · [How-To Guide](HOW-TO.md)

## Use 2 · Choose the DAC Your Sound Goes To

Open **Input/Output · Diagnostics (입출력 · 진단)** (⌘5) in the sidebar and choose **Output DAC (출력 DAC)** and **Output method (출력 방식)**. If your DAC does not appear, plug it in and click refresh (↻). There are three output methods:

- **PCM Direct**: Fidenne leaves the audio untouched and macOS sends it to your DAC. Sound-refining features are turned off. This is the simplest option and works with any device.
- **DSD (DoP)**: The default (starts in PCM Direct until DSD is confirmed on that DAC). The Fidenne engine applies filters and converts to DSD before sending. Your DAC must support DSD.
- **PCM oversampling (PCM 오버샘플)**: Sends engine-processed audio as integer PCM. Suited for DACs that do not support DSD. Choose the output rate from the supported 44.1 – 768 kHz rates under Advanced › PCM; the default for a new setup is to match the source rate.

Sound refinement runs on 2-channel DACs that accept at least one supported rate between 44.1 and 768 kHz. Devices that do not are marked `· PCM Direct only` at the end of their name in the list. For built-in speakers · 3.5 mm jack · AirPods · HDMI, Fidenne processes and sends audio without this label. At the end, macOS mixes it through the system mixer, so it is not bit-perfect (**via system mixer · not bit-perfect**).
If you start in DSD and hear loud hissing or static, stop immediately and switch to PCM oversampling. That DAC cannot decode DSD (DoP).
The first time you send DSD to a DAC you have not used with this app before, a confirmation dialog appears once.

More: [User Manual — Output Method](MANUAL.md#71-independent-output-control--output-mode) · [How-To Guide — Changing the Output Device](HOW-TO.md#4-change-the-output-device-dac) · [Changing the Output Format](HOW-TO.md#5-change-the-output-format--dsd--pcm-integer--pcm-direct)

## Use 3 · Turn Down the Volume First

When you press Play for the first time after launching the app, the "Turn the volume down before starting" dialog appears. Lower the volume on your DAC and amplifier to 0 or very low, click **I turned it down, start (낮췄어요, 시작)**, and slowly raise it while listening.
Clicking **Cancel (취소)** starts nothing.

You can turn off this dialog in Settings › **Sound safety (소리 안전)**. Even when turned off, it still asks once for any DAC you are using with this app for the first time.
Be careful when switching to PCM Direct as well. Because the engine’s safe volume headroom does not apply, check your DAC volume before switching.

More: [How-To Guide — Volume Prompt](HOW-TO.md#24-volume-notice-before-sound-starts--turning-output-monitoring-on-and-off) · [User Manual — First Launch](MANUAL.md#1-first-launch--the-five-step-first-run-setup)

## Use 4 · Connect a Service

Choose a service under **Streaming (스트리밍)** in the sidebar (YouTube Music appears only when enabled in Settings › General). Clicking a service shows its name and connection status (● Connected · Not connected · Needs checking) in the page header.

- **Apple Music** — On first use, macOS asks whether Fidenne can control the Music app and read your Apple Music library. Click **Allow (허용)** for both. Even if you decline library access, Fidenne can still read through the Music app. The connection indicator in the header is not a button. If you missed the prompt, turn on Music under Fidenne in System Settings › Privacy & Security › **Automation**.
- **Spotify** — Optional. If you pick tracks in the Spotify app, Fidenne still refines the sound and shows the current track without a key. To use search, playlists, and playback controls inside Fidenne, click the Spotify status pill in the header, enter your Client ID in the window that opens, and click **Connect Spotify (Spotify 연결)** (Install 10 · 11).
- **YouTube Music** — Enable in Settings › General and follow Install 12. Works in Safari · Chrome · Edge. Click the status pill in the header to open a window where you can pick which browser to connect.
- **Turn on the engine (엔진 켜기)** — Click the **Playback Chain (재생 체인)** pill at the far right of the header and turn on the **Engine (엔진)** switch at the top of the popover so audio passes through Fidenne. The engine switch does not start playback by itself, so start a track in the service app or with the play button in the bottom bar. To choose what plays when you turn on the engine, set **After the engine starts (엔진 시작 후)** on the Input/Output · Diagnostics page.

If audio is routed through Fidenne but you hear nothing, check that the input and output on the Input/Output page match what you chose.
Fidenne does not replace your service subscriptions. Tracks always play from each service’s app under your own account.

**If you control Apple Music playback from Fidenne, turn these off in the Music app**

- **Autoplay (∞)** — The ∞ button above Music’s Playing Next list. Turn it off. If you leave it on, Music does not slip in tracks before Fidenne’s queue ends, but after the queue ends Music continues with tracks it picks itself.
- **Shuffle · Repeat** — Turn them off in Music, and use Shuffle · Repeat in Fidenne’s bar when needed.
- **Song Transitions (AutoMix · Crossfade)** — Music › Settings › Playback. Overlapping tracks blur track boundaries, which can throw off track changes and rate matching.
- We also recommend turning off features that alter sound beforehand (**Sound Check** · **Equalizer** · **Sound Enhancer**), as they modify the audio before Fidenne refines it.

More: [How-To Guide — Listening to Apple Music · Spotify with Fidenne](HOW-TO.md#1-listen-to-apple-music-and-spotify-through-fidenne) · [User Manual — Using YouTube Music](MANUAL.md#81-using-youtube-music-chrome-extension)

## Use 5 · Bottom Playback Capsule

The bar always anchored at the bottom of the window is called the playback capsule. It stays on a single row at the same height whether the window is wide or narrow. From left to right:

1. **Service icon** — The app currently producing sound. Only the icon is shown without a label; hover to see the name. Click to open the current track in that service (for YouTube Music, that browser tab).
2. **Album art** — Click to open the large playback view (Album mode). Press **Esc**, click close (×), or click the art again to close it.
3. **Song (곡)** — Title, with Artist · Album underneath. The **heart** right after the title adds the track to Fidenne’s own **Liked Songs (좋아요한 곡)** (in your Fidenne library), separate from likes in the service app.
4. **Shuffle · Previous · Play/Pause · Next · Repeat** — Shuffle and Repeat apply only to queues played from Fidenne.
5. **Playback position (재생 위치)** — The thin line beneath the track info and playback buttons. Click or drag to scrub. Hovering thickens the line, dims the text just above it, and shows elapsed and remaining time above both ends.
6. **⋯** — Menu for the current track. Depending on the track, you will see **Play Next (재생 대기)** · **Add to End of Queue (대기 목록 끝에 추가)** (when playing a Fidenne queue) · **Add to Playlist (플레이리스트에 추가)** · **Show Lyrics (가사 보기)** · **Track Info (곡 정보)** · **Open in Another App (다른 앱에서 열기)**, followed at the bottom by **Sleep Timer (취침 타이머)** and **Output Settings… (출력 설정…)** (the Output settings from the Input/Output page).
7. **Volume (speaker)** — Click to mute, and click again to unmute. Hover to reveal a volume bar above it; you can also swipe up or down to adjust it. Because this button reads and adjusts the hardware volume of the DAC itself, it appears dimmed on DACs that can only be adjusted with a physical knob, and hovering explains why.
8. **Play Next (다음 재생)** (list icon) — Opens and closes the Play Next · Lyrics panel.

If you narrow the window considerably, the album art becomes square; narrow it further, and Shuffle and Repeat move off the bar into the **⋯** menu.

**The engine switch and output method live in the header, not the bottom bar.** The **Playback Chain (재생 체인)** pill at the far right of the page header shows “App → Output method → DAC” (e.g., PCM 24-bit), with a dot for engine status (green on · gray off · red error). Click it to open a popover with the **Engine (엔진)** switch at the top, **Output settings (출력 설정)** (recommended presets and saved presets) below it, the audio stages, and **Open Input/Output · Diagnostics (입출력·진단 열기)** at the bottom. Hold **Option** while clicking the pill to toggle the engine without opening the popover. If the engine is off and there is an error, a red `!` appears at the far right of the bar; clicking it opens the Input/Output · Diagnostics page.

More: [User Manual — Bottom Playback Bar](MANUAL.md#22-bottom-playback-bar)

## Use 6 · Streaming Page

Open **Streaming (스트리밍)** (⌘1) in the sidebar. Click Apple Music · Spotify · YouTube Music under **Streaming (스트리밍)** in the sidebar and search for songs, artists, or albums.
Home shows **Continue listening (이어 듣기)** · **Played today (오늘 들은 것)** · **My Playlists (내 재생목록)** · **Often played before (예전에 자주 듣던)**.

Spotify search results are not mixed with other services; click the **Spotify** tab at the top of the results to view them separately. Click a track to choose Play Now or Play Next.
If Spotify search does not work, check that you entered your key (Install 10 · 11). If YouTube Music says "Not connected", follow Install 12.

More: [User Manual — Streaming Page](MANUAL.md#3-streaming-page)

## Use 7 · Fidenne Library

Click **⋯** at the end of a track row (or right-click) and choose **Add to Playlist (재생목록에 추가)**. The heart adds it to your Liked Songs list. Use **+ New Playlist (＋ 새 재생목록)** to name and create a new playlist.

Playlists are stored inside Fidenne, while tracks play from their respective services. If a track is removed from a service, that row in your playlist may not play.
Music files on this Mac can be gathered by adding folders on the **Local (로컬)** page in the sidebar. It reads WAV · AIFF · FLAC · ALAC · AAC · MP3 · Opus without moving or modifying the files themselves.
Deleting a playlist leaves your audio files untouched.

More: [User Manual — Track Menu](MANUAL.md#27-track-menu---and-right-click) · [Local Page](MANUAL.md#4-local-page)

## Use 8 · Play Next and Lyrics Panel

When you open Album mode, the middle column holds **Play Next (다음 재생)** (the current track and upcoming tracks) and **Lyrics (가사)**. In Lyrics, the line currently being sung is highlighted clearly and lines farther away fade out.
You can also link a lyrics file (LRC or TXT) directly to a track, or nudge the timing slightly if the lyrics run ahead of or behind the music.

The first time you look up lyrics online, Fidenne asks for consent once. Only **Song Title · Artist · Album · Length** are sent; no audio or account info is ever sent. If you do not agree, nothing is sent.
If lyrics do not appear, click refresh (↻). Tracks that could not be matched are not queried again for 30 minutes.

More: [User Manual — Lyrics](MANUAL.md#23-lyrics) · [How-To Guide — Showing Lyrics](HOW-TO.md#17-view-lyrics)

## Use 9 · Refining Sound

Open **DSP** (⌘4) in the sidebar. Under the DSP group in the sidebar, **EQ** · **Ostrum** · **Crossfeed (크로스피드)** each have their own page.

- **Equalizer**: Adjusts the level of high and low frequencies band by band.
- **Ostrum**: Fidenne’s own feature for shaping bass, presence, and soundstage width.
- **Crossfeed (크로스피드)**: Blends a small amount of left and right channels for headphones. Toggle it on or off with the switch.

Changes **take effect immediately** without saving. There is a brief delay before you hear them as audio passes through the filters and output buffer—up to a few seconds with long filters or the 'Stable' buffer. To keep your changes across launches, click **Save (저장)** (⌘S). If you do not save, they revert when you quit and reopen the app.
Because DSP only runs when audio passes through the engine, the sound will not change if you are on PCM Direct or using a device that accepts none of the 44.1 – 768 kHz supported rates. In that case, see Use 2.
If the sound gets too loud, you may have boosted EQ too much—try lowering it first.

More: [User Manual — DSP Page](MANUAL.md#6-dsp-page) · [How-To Guide — EQ](HOW-TO.md#9-build-an-eq-by-hand-apply-it-and-save-it) · [Crossfeed](HOW-TO.md#12-reduce-the-left-right-separation-in-headphones--crossfeed)

## Use 10 · When Stuck

If there is no sound, look up your symptom in the [Troubleshooting Guide](TROUBLESHOOTING.md). Check three things first: whether the dot on the Playback Chain pill at the far right of the header is green (engine on), whether the volume on your DAC and amplifier is turned up, and whether the volume prompt dialog is open.

If that still does not help, open **Help › Create Diagnostics for a Problem Report…** from the menu. If you agreed to «Diagnostic records for problem reports» on first launch, recording is already running, so create the bundle right after the issue occurs and before quitting the app. If you left it off, click **Start Diagnostic Recording (진단 기록 시작)** and create the bundle next time the issue happens. The app shows you the contents before sending.
**Send by Email (메일로 보내기)** opens your Mail app with the address, subject, and template filled in. If you use another email client (such as Gmail), click **Copy Email Form (메일 양식 복사)** to copy and paste the same text, and attach the bundle yourself. The app never sends anything on its own.

Send inquiries to **fidenne.support@gmail.com**. Include your DAC, output method, and when and what you were doing when you heard the issue. Your app version and macOS version are automatically included in the form and bundle.
The bundle contains timestamps, service, sample rate, and random per-track labels; song title, artist, and album are redacted. Send diagnostic bundles **only by email**, never on GitHub issues.

More: [Troubleshooting Guide](TROUBLESHOOTING.md#9-if-that-still-does-not-work--what-to-collect-and-send) · [How-To Guide — Getting the Beta and Reporting Issues](HOW-TO.md#30-get-the-beta-and-report-a-problem)
