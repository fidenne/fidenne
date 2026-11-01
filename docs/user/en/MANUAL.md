<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/MANUAL.md (0.7.0 edition) -->

# Fidenne User Manual

## One-page summary

**What Fidenne is** — a Mac app that refines the sound of the music app you already use with DSP and sends it to your external DAC. Choose EQ, Ostrum, crossfeed, filters and an output mode suited to your DAC, and check the sound’s path in Playback Chain. Control the service app you already use from Fidenne and view track information and lyrics alongside it (playback stays in each service’s own app). It can also process music files on this Mac. It needs an Apple silicon Mac, **macOS 15 or later**, and, recommended, an **external DAC** (Fidenne processes the sound and sends it to built-in speakers · AirPods · HDMI too).

The app's screens come in Korean, English and Japanese (English and Japanese are AI drafts no native speaker has reviewed). Names are given in English with the Korean original in parentheses.

**Sidebar** — **Streaming** (⌘1), **Local** (⌘2), **Listening History** (⌘3), the **DSP** group (**EQ** is ⌘4), **I/O · Diagnostics** (⌘5), and **Lyrics**. EQ, Ostrum, Plug-ins, Crossfeed, Convolution and DSP Helper each have their own page in the DSP group.

- **Streaming (스트리밍)** — pick a service, search and play, and resume from the home screen. ([§3](#3-streaming-page))
- **Local (로컬)** — reads the music folders on this Mac and shows them as songs · albums · playlists. ([§4](#4-local-page))
- **Listening History (청취 기록)** — view what you listened to by period and source, and export it. ([§5](#5-listening-history-page))
- **DSP** — separate EQ (including AutoEQ), Ostrum, Crossfeed, Convolution (IR), Plug-in (Audio Unit effects) and DSP Helper pages. ([§6](#6-dsp-pages))
- **I/O · Diagnostics (입출력 · 진단)** — output mode, input and output devices (DAC), filter · DSD conversion, and the path the sound takes now. ([§7](#7-io--diagnostics-page))

**The three output modes** (`I/O · Diagnostics › Output mode (출력 방식)`, [§7.1](#71-independent-output-control--output-mode))

- **PCM Direct** — Fidenne does not process the sound. It goes playback app → macOS → DAC as is. The rate is not matched track by track but set once at start; if the rates differ, macOS converts.
- **PCM oversampling (PCM 오버샘플)** — Fidenne raises the sound with a filter and sends integer PCM (24 · 16-bit). Choose from supported rates in the 44.1 and 48 kHz families (44.1 to 768 kHz). A new configuration keeps the source rate; check the actual output in Playback Chain.
- **DSD (DoP)** — Fidenne processes the sound and sends it to the DAC as DSD.
- With EQ · Ostrum · Crossfeed · Convolution off, DSD and PCM oversampling apply no tone-changing processing, but the conversions that format needs (upsampling filter · DSD modulator · dither · headroom) still run.

**Mind the volume** — the first time you play, start with the DAC · amplifier volume low and raise it slowly while listening ([§1](#1-first-launch--the-five-step-first-run-setup)).

**Where to get help** — step-by-step tasks are in the [task-by-task instructions](HOW-TO.md), the first install is in the [install and use guide](../GUIDE.md) (Korean only), when something fails see the [Troubleshooting Guide](TROUBLESHOOTING.md), questions you may have are answered in [Questions and answers](EXPLANATIONS.md), and what the app cannot do yet is in [Known limitations](KNOWN_LIMITATIONS.md). To report a problem, see [§10](#10-sending-a-support-file) and [Beta notice and where to report](#beta-notice-and-where-to-report). **[Experimental]** (〔실험〕) marks an option the app itself labels "experimental".

## 0. At a glance

The path the sound takes: the sound of a playback app (received through Fidenne Inlet or the system tap) or the music files on this Mac → Fidenne (EQ · Ostrum · crossfeed · convolution/IR) → DSD (DoP) or PCM (44.1 to 768 kHz) → DAC. Fidenne processes PCM sound with EQ · Ostrum · crossfeed · filters and sends it to built-in speakers · the 3.5 mm jack · AirPods · HDMI too. macOS mixes the result through its system mixer before sending it to the device, so it is **not bit-perfect**. **PCM Direct** is playback app → macOS → DAC and does not pass through Fidenne.

### What Fidenne does and does not do

It is built to follow each music service's terms and policies, and is changed when they change. The same text is the fourth step of the first launch, and you can read it again from the app menu › **Fidenne이 하는 것 · 하지 않는 것** (What Fidenne does and does not do).

**What it does**

- It takes the playback app's sound through the audio features macOS opens to apps (CoreAudio · audio capture), shapes it in real time and sends it to the DAC you chose.
- It reads the current track through the AppleScript the Music · Spotify apps offer themselves, and passes on play · pause · track skip.
- It reads the Apple Music library and catalogue through Apple's MusicKit (Apple Music API), only when you allow it.
- For YouTube Music, the bundled Safari extension or a Chrome · Edge extension you install reports the open tab’s track inside this Mac.
- Spotify search · playlists · playback control (Spotify Web API) turn on only when you enter the key of your own Spotify developer app.
- Listening history counts the current track the playback app shows through AppleScript (title · artist · album · length) and the time listened — local files by their file tags. It stays on this Mac and is never sent out.

**What it does not do**

- It does not save the sound or make files of it. There is no recording feature.
- It does not replace or bypass a music service subscription. Tracks play through each service's app and your account.
- It does not block or skip any service's ads. Play counts and ads stay with each service.
- There is no server run by Fidenne. Service login details go only to that service.
- It does not mix Spotify search results with other services' results on one screen.
- It does not use what the Spotify Web API gives for cross-service track links · listening statistics · sending to other services.
- No ads and no sales. No analytics · advertising SDK.

### What Fidenne uses

Fidenne is a free app made by an individual and is not affiliated with Apple, Spotify or Google. Apple Music is a trademark of Apple Inc., Spotify of Spotify AB and YouTube Music of Google LLC.

- **Apple Music** — Fidenne drives the Music app through macOS automation. It reads the library list through Apple's Apple Music connection; for a track you listened to (Apple Music · Spotify · YouTube Music) it asks the Apple Music catalogue for other spellings and the same song, and uses the answer in memory only, while the app runs, to find lyrics and link the same song (the catalogue's answer is never kept). To follow each track's source rate it reads the Music app's audio log lines (not kept).
- **Spotify** — Fidenne drives the Spotify app through macOS automation. Search and playlist screens use only a Spotify developer key you create yourself (optional).
- **YouTube Music** — a browser extension reads the track on the open page and passes on controls such as play and pause. It never browses the site on its own: one press by you opens that one page. It never touches ads. Experimental.
- **Lyrics** — LRCLIB (lrclib.net). A `가사 제공 LRCLIB` (lyrics by LRCLIB) line shows under the lyrics. Lyrics belong to their rights holders.
- **Headphone measurements** — public measurement data from squig.link, used for correction. The data belongs to each measurer; the app shows the measurer's name and a link to the original graph.
- **Song search and charts** — Apple's public search and charts. A search is sent at most once every 4 seconds, and the results and pictures stay in memory until the app quits (never kept on this Mac).
- **Sound** — taken from macOS audio and processed only on this Mac. Never recorded or sent anywhere.
- **Kept on this Mac** — ordinary artwork and the lyrics lookup cache expire thirty days after last use. Spotify artwork and information expire thirty days after receipt. Lyrics and translations saved in the Lyrics tab stay until you delete them.

The full list is in [Privacy](../../../PRIVACY.en.md).

**Window layout** — the sidebar contains Streaming, Local, Listening History, DSP, I/O · Diagnostics and Lyrics. ⌘1, ⌘2, ⌘3, ⌘4 and ⌘5 open Streaming, Local, Listening History, EQ and I/O · Diagnostics respectively. Changing sidebar order does not change these shortcuts. The gear-shaped **Settings… (설정…)** row at the bottom opens the Settings window, and the **GitHub** row opens the public repository page. The sidebar header shows only the name Fidenne; the version and build number are in the app menu › About Fidenne and in Settings › General. The window reopens at its last size and position, on the page you last viewed.

## 1. First launch — the five-step first-run setup

On first launch the "Fidenne 처음 설정" (Fidenne first-run setup) window appears. Move between steps with **Back (뒤로) / Next (다음)**.

1. **The DAC the sound goes to (소리가 나갈 DAC)** — pick the output device. "Choose later (나중에 고르기)" also works. If the device does not show, plug in the DAC and refresh.
   Use a USB DAC with its **USB mode on UAC 2.0** and **its own EQ off**. UAC 1.0 stops at 96 kHz, too low to carry DSD; an EQ inside the DAC computes the PCM again, so it cannot pass DSD (DoP) untouched and lowers the rates the DAC takes (the FiiO K15 stops at 192 kHz with its EQ on). Then DSD and the selected PCM 352.8 kHz output do not start (PCM works if you lower the output rate to one the DAC takes). Fidenne's own EQ works together with DSD. Fidenne processes the sound and sends it to built-in speakers · the 3.5 mm jack · Bluetooth · HDMI too without these settings; macOS mixes the result through its system mixer before sending it to the device ([§7.1](#71-independent-output-control--output-mode)).
2. **How to bring in the sound (소리를 가져오는 방법)**
   - **Fidenne Inlet** (recommended, chosen from the start) — receives the playback app's source rate as is. If it is not installed, press **Install… (설치…)**. macOS asks once for the administrator password and restarts the audio service, so all sound stops for a moment. You can also install it later on the I/O page.
   - **System tap (시스템 탭)** — works right away without installing. Receives at 48 kHz.
   - If you already use another loopback app, pick it later under **+ Other input device (+ 다른 입력 장치)** on the I/O page.
3. **What macOS will ask (macOS가 물어볼 것들)** — permissions are not asked now; macOS asks when you first use that feature (system audio · microphone · automation · media library). The screen says when each is asked and what does not work if you decline. Until the first-run setup is over, nothing is sent to Music or Spotify, so neither the automation prompt nor Music launching by itself happens before then.
4. **What Fidenne does and does not do (Fidenne이 하는 것 · 하지 않는 것)** — read what Fidenne uses, what it does and what it does not do (the same text as in [§0](#what-fidenne-does-and-does-not-do)).
5. **Licence and internet connection (라이선스와 인터넷 연결)** — below the full terms are four boxes: **Agree to all (전체 동의)** · **[Required] I agree to the terms of use ([필수] 이용 약관에 동의합니다)** · **[Optional] Use internet features ([선택] 인터넷 연결 기능 사용)** · **[Optional] Diagnostics log for problem reports, kept on this Mac only ([선택] 문제 제보용 진단 기록(이 Mac에만 저장))**. **Start (시작)** works only after the required box. Without the optional boxes playback still works; only features that use the internet are off. **Quit without agreeing (동의하지 않고 종료)** quits the app. You can change the choices later in Settings › Privacy.

**Did it work** — the same window shows the sidebar and a page, and the setup does not appear again on later launches.

**The first time you play — the volume notice.** Each time the app starts, the first press of play shows one sheet "음량을 낮추고 시작하세요" (Lower the volume before you start) **before** any sound. Turn the DAC · amplifier volume to 0 or very low, press **낮췄어요, 시작** (I lowered it, start) (Return), then raise it slowly while listening. **Cancel (취소)** (Esc) starts nothing. It also appears once when you start with a DAC used for the first time ("○○을 처음 씁니다"). The only place to turn this notice off is Settings › **Sound safety (소리 안전)**, and even then it asks once for a new DAC.

**Output watch.** If a signal appears that music cannot produce (sound stuck at one extreme · large DC · a large inaudible ultrasonic signal), Fidenne mutes the rest of that playback and shows "출력을 음소거했습니다 — …" (Output muted — …) at the window's top. Stop and play again to get sound back. Ordinary sound is not changed.

**Internet.** Features that use the internet are turned on and off one by one in Settings › Privacy › **Network destinations (네트워크 목적지)**. With all of them off, receiving sound · DSP · DSD conversion · DAC output · file playback still work, and sound never leaves the Mac.

**When startup fails twice in a row** — on the third start a `시작 복구` (Startup recovery) window appears. **안전하게 시작** (start safely) enters with the engine · capture · browser extension · auto-play connections off for this one run (`안전 시작 중`, safe start, is shown) and does not erase any setting. The next run goes back to normal. **진단 만들기…** (make diagnostics) builds the material to send from the diagnostics already saved, and **그대로 시작** (start as usual) starts normally. A forced quit after a normal start, quitting yourself, and a restart for an update are not counted as failures.

## 2. Always visible — header · bottom playback bar · menus

### 2.1 Page header

The **Playback Chain** button next to the page name shows the order the sound passes — **source → capture → conversion → band → DSP → filter → output → device** — one line each, with the current values.

- The dot and word in its header give the overall state: **Running · processed (실행 중 · 처리됨)** · **Running · no processing (실행 중 · 처리 없음)** (PCM Direct) · **Stopped (멈춤)** · **Preparing (준비 중)** · **Error (오류)**.
- The **source** line is the app making the sound now, the **capture** line is how and at what rate it is received (red if sound was dropped). The **conversion** line says whether the original and received rates match; if not, in red `44.1 kHz → 48 kHz · 재생 앱이나 macOS 가 바꿈` (changed by the playback app or macOS). Spotify does not report its original rate, so it reads `없음으로 추정` (assumed none).
- The **band** line measures where the incoming sound is cut off (for example `16.0 kHz 위로 소리가 거의 없음`, almost no sound above 16.0 kHz). It does not say why — it may be lossy compression or a trait of the original master.
- A chip on the **DSP** line (**EQ · Ostrum · Crossfeed**) is a single button. Pressing it opens that setting's panel right there, and pressing it again folds it. Turning it on and off is done with the **switch** beside the name in the panel's first row (the dot on the chip is only a status mark). Under PCM Direct, or when the engine reports no values, the switch is dimmed and the reason is shown with it. A line ending in `›` takes you to that setting.
- If the output device is missing or disconnected, that line turns red and **Find again (다시 찾기)** · **Reconnect (다시 연결)** appear.
- When several stages are open and the window would be taller than the screen, the popover scrolls and follows the stage you just opened into view. A long name in a list (a headphone or device) scrolls while the pointer is on it, so you can read it to the end.

When something goes wrong, a red notice band appears at the window's top (for example `DAC 연결이 끊겨 재생을 멈췄습니다. 다시 연결한 뒤 재생을 누르세요.` — the DAC was disconnected, so playback stopped; reconnect it and press play). It closes by itself when the DAC comes back, or with ×.

### 2.2 Bottom playback bar

The bar floats on every page. It is one row at any window width and its height never changes: service icon · album cover · track (title · heart / artist · album) · playback buttons (shuffle · previous · play/pause · next · repeat) | ⋯ · volume (speaker) · **Up next (다음 재생)**. In a narrower window the cover becomes square, and in a still narrower one shuffle and repeat leave the bar and move into the ⋯ menu. The engine switch and the output mode are not in the bar: they are in the **Playback Chain** pill at the right end of the page header (below).

- **Position** — the line under the track and the playback buttons. Press or drag it to move. When the pointer rests on it, the line thickens, the row right above it blurs and the elapsed and remaining times appear over its two ends.
- **Heart** — adds to Fidenne's own **Liked songs** in the library, separate from the service app's likes.
- **Service icon** — the app making the sound now. Only the icon shows, without a name; resting the pointer on it shows the name. Pressing it opens the current track in that service (for YouTube Music, its browser tab). When the Spotify app is not installed on this Mac, Spotify's official icon shows instead (black on light screens, white on dark ones).
- **Playback Chain pill** (right end of the page header) — its text is `app → output mode → DAC` (a narrow header drops the DAC, then the app, first), and its dot is the engine state (green on · grey off · red error). Pressing it opens a window: the **Engine** switch at the top · **Output settings** (recommended sound presets · saved presets · custom) · the stages the sound passes through · **Open I/O · Diagnostics**. Choosing a saved preset switches to its output mode. Pressing it with **Option** held turns the engine on or off without opening the window.
- **⋯** — the track menu ([§2.7](#27-track-menu---and-right-click)) with a **Sleep timer (취침 타이머)** and "Output settings… (출력 설정…)" (the output settings on the I/O page) added. In a narrow window shuffle and repeat are also at its top.
- **Up next (다음 재생)** — opens and closes the Up next · Lyrics column.
- **Previous** — when you listen to a Fidenne list with Apple Music or Spotify, pressing it after 3 seconds or more of the song goes back to the start of this song; within the first 3 seconds it goes to the song before (on the first song of a list it returns to the start).
- **DAC volume (DAC 음량)** — the speaker button in the bar mutes and unmutes when pressed, and a slider appears above it when the pointer rests on it. The button and the slider read and change the DAC's own volume (it is not a separate Fidenne volume). Only values read from the device are shown, and if it cannot change the volume you see `DAC 음량을 바꾸지 못했습니다. 장치에서 읽은 값을 표시합니다` (could not change the DAC volume; showing the value read from the device). When the speaker is dimmed, hover for the reason: `DSD · 정수 출력 중에는 DAC 본체 노브로 조절합니다` (during DSD · integer output use the DAC's own knob; Fidenne then takes over the DAC volume and holds it at maximum) · `이 DAC 는 본체 노브로 조절합니다` · `이 DAC의 음량 속성은 읽기 전용입니다` · `출력 상태를 확인하는 동안 음량을 조절할 수 없습니다`. Details: [Troubleshooting guide](TROUBLESHOOTING.md#dac-volume-and-dsd-dop--integer-pcm)
- **Engine switch** — the **Engine** row at the top of the Playback Chain window. It turns Fidenne's processing (the engine) on and off. The pill's dot is the state (green running · grey off · red error). When the engine is off with an error, a red ! appears at the right end of the bar; pressing it opens the I/O · Diagnostics page.
  - **The engine switch does not start a track, and the play button does not turn the engine off.** Pause stops only the playback app, and **Play** with the engine off turns it on and plays.
  - What plays when the engine starts is set by **After the engine starts (엔진 시작 후)** on the I/O page ([§7.3](#73-streaming-app-autoplay--input-and-output-devices)).
- Shuffle · repeat work only on lists played from Fidenne. Another app's queue is handled in that app.
- Click a song list's **#** · **Title (제목)** · **Album (앨범)** · **Time (시간)** head to sort by that column ascending; click again for descending, and once more for the list's own order (the sorted head shows ↑ ↓). Anywhere in the head's box works. **#** returns to the list's own order. It is the same state as the list's **Sort (정렬)** menu, playback follows the order on screen, and it is forgotten when the app quits.
- When a browser or another app starts making sound, the bar says **`시스템 소리 — 출처를 모름`** (system sound — unknown source), and meanwhile it does not count history or look up lyrics.
- When Spotify plays on another device (a phone etc.), the bar shows only **`Spotify — 다른 기기에서 재생 중`** (playing on another device). Control it on that device. If content scrolling behind the bar hides its text, change the material in Settings › General › **Playback capsule (재생 캡슐)** (macOS 26 — on macOS 15 the capsule is always opaque, so nothing shows through).

**Large playback view** — press the album cover in the bar. It has three columns: cover and controls · **Up next (다음 재생)** and **Lyrics (가사)** · **Playback Chain** (fold it with the `›` grip or **⌥⌘P**). **⌘F** searches over this view, and the service name (`Apple Music ↗` etc.) opens the current track in that service. Close with ×, by pressing the cover again, or **Esc**.

**Up next and Apple Music** — Apple Music does not tell other apps its upcoming tracks.

- When you play an Apple Music list from Fidenne, it alternates between **‘Fidenne 재생 대기열’** and **‘Fidenne 재생 대기열 2’** in the Music library. It fills the current track and the whole remaining list in order. Before first use it asks once (**Continue** or **Turn off and continue**). With iCloud Library on, these playlists also appear on your other devices. Turn it off in Settings › Privacy › Apple Music › **Advance tracks through a Fidenne playlist**.
- For a track you started in the Music app, Fidenne reads which playlist · album it came from and shows the next tracks. If it cannot tell, **Continue this album (이 앨범 이어 듣기)** · **Back to the Fidenne list (Fidenne 목록으로 돌아가기)** · **Leave it to Apple Music autoplay (Apple Music 자동 재생에 맡기기)** appear.
- When Music picks another track by itself, **`Apple Music 자동 재생이 고른 곡`** (a track picked by Apple Music autoplay) appears. The whole Fidenne list is in Music's playlist, so this does not happen before the list ends even with autoplay (∞) on; if it still does, turn autoplay (∞) off.


**If Fidenne controls Apple Music playback, turn these off in the Music app**

- **Autoplay (∞)** — the ∞ button above Music's Up Next. Music picks tracks only after the Fidenne list has ended (with "continue with Apple Music autoplay when the current list ends" on, it carries on from there).
- **Shuffle · Repeat** — turn them off in Music; use the shuffle · repeat on Fidenne's bar if you need them.
- **Song transitions (AutoMix · Crossfade)** — Music › Settings › Playback. Overlapping tracks blur when a track changes, so track changes and rate matching can go wrong.
- Things that change the sound first (**Sound Check** · **Equalizer** · **Sound Enhancer**) are best turned off too; they change the sound before Fidenne shapes it.

### 2.3 Lyrics

When a track plays, the lyrics panel shows its lyrics. Internet lyrics (lrclib.net) need your consent once — "동의하고 찾기" (Agree and search) / "보내지 않음" (Do not send). Only the title · artist · album · length are sent.

| Control | What it does |
|---|---|
| **Link lyrics file (가사 파일 연결)** | Links an LRC · TXT file to this track (can be unlinked). |
| **Lyrics timing (가사 타이밍)** (clock button) | Opens from the clock button. + if lyrics are early, − if late. Applies to this track only and is remembered. |
| **Text linking (글자 연결)** | Fits an untimed lyrics file's text to the timing of the current lyrics. |
| **Korean translation (한국어 번역)** | Adds a Korean line under each line. Without a Korean version it fills in a translation. It tries AI lyrics translation (if you turned it on) → the Apple model on this Mac → macOS translation → the original, in that order (**Translation steps (번역 단계)** in the sidebar's **Lyrics** tab, [§8](#8-settings-window)). |
| **Pronunciation line** | Writes how a line is read in letters under the original. Turn on the eye of the **Pronunciation** line in the sidebar **Lyrics (가사)** tab › **Display (표시) › Line order · Visibility (줄 순서 · 보이기)** (off by default). With a Korean screen, Japanese · Chinese lyrics get Hangul readings; with other screen languages, romaji (Japanese) · pinyin (Chinese) · romanization (Korean lyrics). A Korean lyric has no pronunciation line on a Korean screen. The reading is macOS's **estimate** (`Pronunciation lines are estimates`), so kanji readings or sound changes can be wrong. In the Lyrics tab, click a line to edit it yourself (Return saves, Esc cancels); it stays as `Pronunciation I edited`. |
| **Line order** | Original → pronunciation → translation by default; drag items or press ⌥⌘↑ · ⌥⌘↓ to reorder. The eye shows or hides each line, and at least one must stay shown. The order applies to the lyrics panel and the album screen; the Lyrics tab is where translations are edited, so its translation column is always shown. |
| **Lyrics version (가사 판)** | Appears when two or more versions are known; picks one (original · romanized · English · Korean etc.). Find others with **Other version (다른 판)** in the source line. |
| Refresh (↻) | Searches once more. |

- Text size is set in **Display (표시)** in the sidebar's **Lyrics (가사)** tab (small · normal · large).
- **Lyrics tab (가사)** — the last row of the sidebar, where the lyrics and translations of tracks you have heard are kept. The chips at the top (**All · Apple Music · Spotify · YouTube Music · Local** — the YouTube Music chip shows only while **YouTube Music (experimental)** in Settings › General is on) filter the list by service, and search works inside the chip you chose (it also matches the title and artist of that song's other versions). Choosing a song shows the original and the translation side by side, line by line, and a translated line can be pressed to edit it. Below are four groups of settings — **Display (표시)** (text size · translation lines · translation language · tone · extra request) · **Translation steps (번역 단계)** (AI provider → Apple model on this Mac → macOS translation; the key and limits are in the collapsed **AI provider settings**) · **Lyrics source (가사 출처)** · **Storage (보관)**. Lyrics and translations stay on this Mac and the app never deletes them by itself. An older saved lyric also appears in this tab once you play that song again — for an older lrclib.net lyric that had no record number, the app asks once for the number while that song is playing (if lyrics internet search is on; even with the lyrics window closed, for a song from any service) and keeps it in the list together with the translation you had saved.
- **When the lyrics server refuses** — you see `가사 서버(LRCLIB)가 요청을 잠시 거부했습니다. …` (the lyrics server, LRCLIB, refused requests for a while; this happens after many requests in a short time; no new request for about N minutes; turning lyrics search off and on in Settings resumes at once). Wait, or connect an LRC · TXT file.
- **Deleting translations** — a translation made by AI is deleted one song at a time with **이 번역 지우기** (delete this translation) under the lyrics, or all at once with **AI 번역 전부 지우기…** in Settings.
- **Previous Translations** — when **Retry AI Translation** changes a translation, the one from before stays in **Previous Translations**. Choose one (`Restore a previous translation?`) to bring it back, and Undo cancels that. Lines you edited yourself change with it, and if you use an AI provider the cost of requests already made is not refunded.
- Even when an app spells a track differently (a Korean artist name · "- Remastered" etc.), it finds the lyrics if the title · length and the artist or album match. Another person's song with only the same title and length is not shown.

### 2.4 Menu bar icon · menus

- **Menu bar icon** (waveform) — status · start · stop · play/pause · open window · output device · **EQ presets ▸** (the last five; choosing one is heard at once) · quit. Start · stop are the same as the engine switch.
- **Sleep Timer (취침 타이머)** — in the Playback menu, the menu bar menu and the playback bar's menu, choose **15 · 30 · 45 · 60 min · When This Song Ends (이 곡이 끝나면) · Custom… (직접 입력…)** (1 to 720 minutes). At the end it pauses once, like pressing pause yourself (the sound fades as that service's pause does); it never plays again or clears the queue. While time remains the menu title reads `Sleep Timer · ○ min left`; **Turn Off Timer (타이머 끄기)** ends it. Pausing or playing yourself does not cancel it, and quitting the app removes it. The same for the three services and Local.
- **Volume · mute** — in the Playback menu: **Volume Up** (⌘↑) · **Volume Down** (⌘↓) · **Mute** (⌥⌘↓). Esc closes the volume bar.
- **Shortcuts and links** — call six Fidenne actions from the Shortcuts app · Siri · Spotlight: **Play / Pause** · **Next Song** · **Previous Song** · **Song playing now** (returns title · artist · source as text) · **Bypass sound processing** (on / off) · **Choose EQ Preset**. **Bypass on** turns off only the EQ · Ostrum · Crossfeed that were on and changes no saved setting; **off** restores only what it turned off (after a relaunch it remembers nothing and says there is nothing to restore). The links `fidenne://play-pause` · `fidenne://next` · `fidenne://previous` · `fidenne://bypass?on=1` · `fidenne://preset?name=Name` do the same. Output device · volume · output method · engine start/stop · settings · deletion are in neither Shortcuts nor links, and any other link is refused. The same link is not taken twice within 1 s and no more than ten times in 10 s. If the app is not running, the shortcut launches it.
- **Hiding the icon** — turn Fidenne off in **System Settings › Menu Bar › Allow in the Menu Bar**. The window · Dock · shortcuts stay.
- **App menu** — "About Fidenne" (with the trademark notice), **Check for updates… (업데이트 확인…)**. It reads the public repository once and says "최신입니다" (up to date) or names the new version (or says there is no public release yet). For a new version it also shows a few lines of what changed. If you left the GitHub connection on at first run, it also checks every 4 hours without being pressed (and at launch and on wake) and tells you about a new version; if the app is in the background, a notification banner appears once per version and clicking it opens the update window (turn it off with the switch at the bottom of Network destinations). A new version is downloaded only when you choose to install it in the update window; the downloaded version is installed, and Fidenne restarted, only after its signature checks out. For update checks and downloads, github.com may point to `release-assets.githubusercontent.com`, and the update tool (Sparkle) follows that pointer itself. More: [Privacy](../../../PRIVACY.en.md).
- **Help menu** — **Show controls (조작법 보기)** · **Create diagnostics for a problem report… (문제 제보용 진단 만들기…)** ([§10](#10-sending-a-support-file)). **Diagnostics menu** — start/stop diagnostics · **Export support diagnostics… (지원용 진단 내보내기…)** · **Delete saved diagnostics… (저장된 진단 삭제…)**.
- Deletions that cannot be undone (saved diagnostics · a playlist · shortcuts "all to defaults") ask once. The red button is not pressed by Return.
- **Shortcuts** — the list is in Settings › **Controls and shortcuts (조작과 단축키)**: change · clear · default per key. It warns about clashes with macOS shortcuts. They work only while the Fidenne window is in front (media keys excepted).
  **⌘S** saves the Equalizer or Ostrum on screen, and **⌘F** goes to the page's search field on Library · Listening History, otherwise to the Music search field.
  The keys that turn EQ · Ostrum on and off are heard at once but do not save.

### 2.5 Explanations · how to read graphs · glossary

- The line under a section title says what that feature does. Pressing **ⓘ** at its end opens a bubble: when to use it · what to put in · what changes · the cost. **Esc** or a click outside closes it.
- **Glossary (n) (용어 풀이)** in an explanation shows that part's terms, and **Show the whole glossary (용어집 전체 보기)** shows all of them, including IR (impulse response), convolution and true stereo. Under each graph the axes and line names are always visible; **ⓘ** at the end of that line explains each line, how to read it and what the graph cannot tell.
- Numbers in the app come from measurements, and the app never judges that a setting makes the sound better.

### 2.6 Handling knobs · sliders · EQ points

The first time you open Equalizer and Ostrum, a tip **EQ 다루기** (Handling the EQ) · **노브 다루기** (Handling knobs) appears next to the control once. To see it again: **Help › Show controls**, or Settings › Controls and shortcuts › **Show tips again (팁 다시 보기)**.

| Control | How |
|---|---|
| Knob (Ostrum) | Drag vertically or horizontally (up or right = more). **Shift** · **⌥** fine-tune. **Double-click** or ⌥-click resets it. Press the number to type a value |
| EQ slider | Press or drag up and down. **Double-click** · ⌥-click is 0 dB |
| EQ number field | Press, type, **Return**. The arrows step one notch. ⌥-click is the default |
| Graph point (EQ) | Dragging changes frequency and gain together. **Shift** · **⌥** move ten times slower. Pressing a point selects it; drag the small ring beside it sideways for Q. Double-click empty space to add a band |
| Position · other sliders | Press or drag |

- **Two-finger scrolling** always moves the page. A value changes only when you keep **⌘ held** with the pointer on the control (scroll up = up); add ⌥ · Shift for slower. Choose the behavior in Settings › Controls and shortcuts › **Change values with two-finger scrolling (두 손가락 스크롤로 값 바꾸기)** (with ⌘ held · when started over a control · off).
- **Trackpad haptics** — **Off · ends only · normal (끔 · 양끝 알림 · 일반)** in Settings › Controls and shortcuts. On a Force Touch trackpad a light tap per notch while dragging.
- **Streaming page back · forward** — the ‹ › buttons, ⌘[ ⌘], a sideways trackpad swipe and the **mouse side buttons** (back · forward) all make the same step. The side buttons work only while the Fidenne window is in front.
- **⌘Z / ⇧⌘Z** — step back and forward through changes made on the DSP page (one whole drag is one step). Undone values are heard at once.

### 2.7 Track menu — ⋯ and right-click

Wherever a track is a row (Music · Up next · Library · Listening History), **⋯** at the row's end or a **right-click** opens the same menu. Items that cannot be done for that row are not shown.

1. **Play (재생)** · **Play next (다음에 재생)** · **Add to end of queue (대기열 끝에 추가)**
2. **Add to playlist ▸ (재생목록에 추가)** · **Show lyrics (가사 보기)** · **Track info (곡 정보)** · **Open in Apple Music (Apple Music에서 열기)** · **Show in playback app (재생 앱에서 보기)** · **Show in Finder (Finder에서 보기)** · **Copy link (링크 복사)** (with two or more places to open, they are grouped under **Open in another app ▸ (다른 앱에서 열기)**)
3. **Remove from playlist… (재생목록에서 빼기…)** (asks once; files stay) · **Remove from queue (대기열에서 빼기)**

Spotify tracks have **Open in Spotify (Spotify에서 열기)** · **Copy link**.

**Choosing rows** — a row in a track list is selected by one click (no playback); a double-click or Return plays it. The ▶ that appears when you point at a row plays with one click. ⌘-click adds or removes one, ⇧-click selects a range, and typing jumps to that title. With several rows selected, the menu keeps only items that fit many tracks (**Add to Playlist** only when they are from the same service). In Fidenne lists and Up next, Delete removes and ⌘Z undoes; in lists a service owns (Apple Music · Spotify · YouTube Music) Delete does nothing. The same for the three services and Local.

<a id="3-music-page"></a>
## 3. Streaming page

Where you search and open Apple Music · Spotify · YouTube Music in one place.

- **Automation prompt** — if you see `시스템 설정의 개인정보 보호 및 보안 > 자동화에서 Fidenne의 Apple Music 접근을 허용해 주세요.` (for Spotify, `Fidenne의 Spotify 접근을…`; allow Fidenne's access to Music in System Settings › Privacy & Security › Automation), turn on Fidenne's Music or Spotify there. After you return to Fidenne it reads the lists again and the notice goes away. If you did not allow it in the first prompt, you can still turn it on in the same place later.
- **Choosing a service** — click **Apple Music** · **Spotify** · **YouTube Music** under **Streaming** in the sidebar (YouTube Music shows only when it is turned on). The dot next to the service name in the page header shows the connection and opens the connection window. YouTube Music needs the extension in [§8.1](#81-using-youtube-music-chrome-extension).
- **Search** — results come on one screen in order: my Apple Music (library · playlists) → the Apple Music catalogue (tracks not in the library) → files on this Mac. The last line **Find ‘query’ in YouTube Music ↗** opens the same search in a YouTube Music tab.
  - **Spotify results are separate** — press the **Spotify** tab at the top of the results, and the **Apple Music · Local** tab to come back. Spotify asks that its content not be placed next to other services' results.
  - **Add to library (보관함에 추가)** — puts a catalogue track · album into the Apple Music library. A confirmation appears the first time (the library changes; with iCloud library it shows on other devices). It takes a while to appear, so "보관함에 나타나는 중" (appearing in the library) shows until the button becomes **Play**.
- **Reorder (순서 조정)** — the **순서 조정** button in the play row of an open playlist or album lets you drag song rows into a new order. Each row also has **위로 옮기기** (move up) · **아래로 옮기기** (move down), and the keyboard uses ⌥↑ · ⌥↓. Press **완료** (done) to finish. While it is on, the **#** column shows your own order numbers, and ⌘Z steps back one move. Only the order inside Fidenne changes; the order of the playlist at Spotify · Apple Music · YouTube Music stays as it is. The button is dimmed for a list of fewer than two songs or one still arriving. If the order cannot be saved you see `순서를 저장하지 못해 이전 순서로 돌아갔습니다` (could not save, went back to the earlier order); if the order file cannot be read, `순서 파일을 읽을 수 없어 순서를 바꿀 수 없습니다`.
- **Save an album to your library** — the **라이브러리** (Library) button in an album's header (**저장됨**, Saved, when it is already saved) saves the album to the service or takes it out. How it is saved differs by service.
  - **Spotify** — the app asks Spotify to save, then reads back and shows only what Spotify confirms. Without the permission you see `앨범 저장 권한을 허용하려면 Spotify에 다시 연결해 주세요.` (reconnect Spotify to allow saving albums); connect again in the Spotify connection window (the dot beside Spotify on the Streaming page).
  - **Apple Music** — it goes into your iCloud library. When the request is accepted you see `보관함에 넣었습니다. Music 앱에 보이기까지 조금 걸릴 수 있습니다.` (added; it can take a while to show in the Music app). The app checks again a few times, and the button becomes **저장됨** once the album shows. If it never shows, you only see `아직 Music 에 보이지 않습니다` (not in Music yet); that is not called a failure. Without permission · a subscription · the iCloud library, one sentence gives the reason and the button goes back to opening the album in the Music app.
  - **YouTube Music** — the app does not save by itself. The extension presses the save control on the open YouTube Music album page once and reports what the page shows (**YouTube Music에 저장**). That album page must be open in the browser. If the result cannot be confirmed you see `저장 여부를 확인하지 못했어요. YouTube Music에서 확인해 주세요.` (could not confirm; check in YouTube Music), and it is not pressed again. A single song is saved the same way.
- **Pressing a track** — **Play next** / **Play now (지금 재생)**. A song row in the search results works the same way. Only when Fidenne is running a list does it ask **how to play (재생 방법)**; with no such list (for example only a song started in the Music app is playing) it does not ask and plays the pressed song at once. **Play all (전체 재생)** · **Shuffle (셔플)** over a list go through it once without repeats. A long Apple Music list may show **재생 준비 중…** (preparing playback…) the first time; to shuffle, turn **Shuffle** on before playing.
- **Home screen** — from the top: **Continue listening (이어 듣기)** (with that day's **Today's listening (오늘의 듣기)** card beside it), **Listened today (오늘 들은 것)** (**Recently listened (최근 들은 것)** when the day on screen is not today), **My playlists (내 재생목록)**, **Often played before (예전에 자주 듣던)**. ▶ on a Continue card plays that card's service and track, from the saved position if there is one. The card follows the track the service's player is holding now (playing or paused), and ▶ turns into ⏸ while that same track plays. **Open list (목록 열기)** opens the list the track was heard from.
  - **Listened today** is one row you swipe sideways through the tracks of the last 7 days (today included). The day changes at 4 a.m., and a line shows where one day ends. The date chips above the row (**Today · Yesterday · Last 7 days (최근 7일) · weekdays**) show the day on screen in a darker tone, and pressing one jumps to that day. While you look at days older than yesterday, the **Last 7 days** chip opens out into the weekdays that have tracks. The row's heading follows the day on screen, **Listened today** or **Recently listened**. Like the rows of a track list, a track tile only selects on one press, and plays on a double press or on Return once selected (the album rows of **Often played before** work the same). A group tile unfolds and folds on one press. Tracks heard in a row from one playlist or album become one tile, and the tile's arrow unfolds the tracks.
  - **See all (모두 보기) ›** at the row's right end does not open another screen; it unfolds the last 7 days as a grid right there. The same tiles sit one line per date, and a group tile unfolds and folds when pressed. While it is unfolded, the row's head (title · **Fold (접기)** · **Stats (통계) ›**) and the date chips stay pinned at the top as you scroll down, so you can press **Fold** or jump to a day from anywhere, and the lit chip follows when you scroll by hand. Double-pressing a track tile plays on from it in the order shown, skipping folded groups. **Stats ›** opens the Listening History page.
  - The **Today's listening** card shows that day's output modes · devices · interruptions and can be folded and unfolded. The interruptions line does not appear for a day that was not measured. Tracks heard through Spotify are not counted in the listening statistics.
  - **Order and hiding of sections** — drag a section header's handle to reorder (⌥↑ · ⌥↓ on the handle also works). The eye button hides a section, and a hidden section comes back from **<name> show again** at the bottom. Playlist tiles can be dragged too. Only the order inside Fidenne changes; the playlists at the services stay as they are.
  - **Drag into a playlist** — drag (more than 4 pt) a song tile · a song inside an opened group · a playlist group · a **Played separately (따로 들은 곡)** group onto a Fidenne playlist · **Liked songs** · a service playlist tile in **My playlists**, or a playlist group on the timeline, and it is added at once without a window. It only copies; lists are never merged or moved. A target that takes it shows a highlight ring and an `Add to ‘Name’` label; one that does not (a **Played separately** group · album · radio group · song tile · date chip · empty space · itself · a list that cannot be written) shows a no-drop cursor and one line of reason (`You can’t drop it here`). If the songs are all there already it says `Already there`. After adding, a toast and **Undo** (10 s, ⌘Z) appear. Only songs of a service go to that service's playlists; for Spotify, press **Allow… (허용…)** once on the first drop into a list you own or co-own, and Apple Music takes a drop only into an ordinary playlist while the Music app is open. YouTube Music service playlists do not take drops. **What is written to a service has no undo button** and the toast says `You can remove it in the service yourself`. Song rows of a service playlist · album and the right-hand queue (Up next) take the same drag.
  - **Group with Another Group of This Day (이 날의 묶음에 묶기)** — groups songs of the same service and day. It is only in the tile's ⋯ menu (not a drag) and appears when a group of that day can take it. A group you made by hand shows as a group from 2 songs within the same day, and songs heard afterward are not merged into it automatically. It applies only to what Home sees; the listening history is not changed.
  - **Remove from History (기록에서 지우기)** — in a song tile's ⋯ menu (or select the tile and press ⌫) it hides that song's repeat entries from Home. `Removed from history` and **Undo** (10 s, ⌘Z) appear, and a group asks once (`Delete this group from history?`, the default button is Cancel). It disappears from Home only and **is not removed from statistics** (`It isn’t removed from statistics`) — real deletion is **Delete listening history** on the Listening History page.
  - Everything dragging does also works without dragging — **Add to Playlist ▸** in the ⋯ menu, the keyboard (←→ to move between tiles, the menu key for the ⋯ menu, ⌫), and VoiceOver custom actions (**Add to Playlist** · **Group with Another Group of This Day** · **Remove from History**).
  - **Library albums (보관함 앨범)** — at the top of **My playlists** (after the Fidenne lists, before the service's playlists) there is one tile such as **보관함 앨범 · 54** (Library albums · 54). Its cover is a mosaic of the first four albums; pressing it unfolds the albums right there (pressing an album opens its album screen) and pressing it again folds them. With no saved albums the tile is absent, and while the albums are first being read only a `불러오는 중…` (loading…) line shows. It is the same for all three services; Spotify's shows only while connected. The open state is remembered per service while the app stays open.

**Connecting Spotify (optional)** — even without a key, when you pick a track in the Spotify app Fidenne shapes its sound and shows the current track. Search · playlists · playback control turn on only with **the key of your own Spotify developer app** and a Spotify Premium account, whose terms you agreed to.

The connection screen shows `연결하면 이용약관 9조(Spotify)에 동의합니다.` (connecting means agreeing to clause 9 of the terms); if you connected earlier, the same notice appears once. Information from Spotify is kept only on this Mac, for up to 30 days. **Disconnect (연결 해제)** asks for confirmation and then deletes tokens immediately and hides Spotify information on this Mac (Spotify tracks in listening history, Fidenne lists, track links and caches) for four days before deleting it. Reconnect within four days to restore remaining data, or use **Delete all now** to erase it immediately. Tracks heard through Spotify are left out of the listening statistics, and the explicit mark (`E`) that Spotify supplies shows in the same place as for the other services. No button is placed on a Spotify cover; press the cover to open it. Spotify covers on the home and in listening history are fetched one song at a time; a song whose cover could not be fetched stays a grey placeholder and is tried again. A refused cover request does not block reading your Spotify library. Closing the login window part-way through connecting leaves an already-connected account connected.

1. Press **Open developer dashboard (개발자 대시보드 열기)** in the connection window (press the dot beside Spotify on the Streaming page, or **Connect (연결하기)** on the Spotify screen) and create an app.
2. Put the address shown in the box into that app's Redirect URI (the **Copy (복사)** button beside it).
3. Paste the dashboard's **Client ID** into the box. Fidenne does not use the Client Secret, so do not enter it, and do not share it with anyone.
4. Press **Check key (키 확인)**, and if it is right, **Connect Spotify (Spotify 연결)**. The Spotify login window opens in the browser.

After connecting you see "Refresh playback permission (재생 권한 갱신)" · "Disconnect (연결 해제)". **Follow Spotify queue · for Jam (Spotify 대기 목록 따르기 · Jam용)** keeps Fidenne from overwriting a Spotify shared queue.

**Did it work** — pressing a track shows its name and service icon in the bottom bar, and the position moves.

<a id="4-library-page"></a>
## 4. Local page

Where you listen to music files on this Mac. Formats read: WAV · AIFF · FLAC · ALAC · AAC · MP3 · Opus (when macOS can read it). `.ogg` · `.oga` do not play yet.

1. The first time, press **Add folder… (폴더 추가…)** and choose your music folder.
2. When indexing is done, find tracks in **Songs · Albums · Artists · Playlists (노래 · 앨범 · 아티스트 · 재생목록)**.
3. Double-click a row or select it and press Return to play from that track.

**Did it work** — rows show cover · title · format (for example FLAC · 96 kHz · 24-bit) · length, and pressing one shows it in the bottom bar.

- **Music folders (음악 폴더)** menu — Add folder… · **Re-index (다시 색인)** · Remove folder from list ▸ (only from the list; files on disk stay).
- **Songs** — the search field (⌘F) filters the current list. A file that cannot play shows the reason (`손상된 파일`, damaged file, etc.) in the format column. **Albums · Artists** are grouped by file tags.
- **Playlists** — enter a name and create one. Inside: Play all · Shuffle · Delete… (deletes only the playlist; files stay). "파일을 찾을 수 없음" (file not found) means a folder was removed or the file moved.
- **Selecting several · reordering** (playlists · Up next) — select with ⌘-click · Shift-click, and drag a row onto another to move it. **Return** plays the first selected track.
- **Up next** — the **Up next (다음 재생)** button in the bottom bar shows the current and upcoming tracks. Tracks of the same rate play without a gap; where the rate changes there is a short break.
- Local files play through the Fidenne engine. PCM Direct keeps the source rate, bypasses sound processing and disables dither.

**YouTube Music playlists** collect not on this page but in `Streaming › YouTube Music › My playlists`. There are two ways in — opening a list screen in the browser ([§8.1](#81-using-youtube-music-chrome-extension)) and a Google Takeout file ([§4.1](#41-importing-youtube-music-playlists)). Fidenne never walks the YouTube Music site by itself. What you can do on an imported track row:

- **Kind** — each track is seen as a song · `뮤직비디오` (music video) · `음악 영상` (music clip) · `음악 아님` (not music) · `종류 모름` (kind unknown). By default **only `음악 아님` is left out**.
- **Include · exclude** — the button at the row's end. Turn on **Show filtered (걸러진 것 보기)** to see left-out tracks too. Your choices stay even when you import again.
- **Track menu** — **Open in YouTube Music (YouTube Music에서 열기)** · **Copy link** · add to / remove from a playlist. These tracks play in a YouTube Music tab.

### 4.1 Importing YouTube Music playlists

Imports YouTube Music playlists and library songs from a **Google Takeout** file. Fidenne asks nothing on the internet and reads only the file you received.

1. Open `takeout.google.com` in the browser and log in.
2. **Deselect all** → check only **YouTube and YouTube Music**.
3. Press **All YouTube data included** on that row and keep only **playlists** and **music**.
4. **Next step** → export once · `.zip` → **Create export**. When it is ready, download it from the link in the email.
5. Double-click the zip in Finder to unpack it.
6. In Fidenne, open **YouTube Music library (YouTube Music 보관함)** at the bottom of `Streaming › YouTube Music › My playlists`, press **Import YouTube Music playlists… (YouTube Music 재생목록 가져오기…)** and choose the whole unpacked `Takeout` folder.

**Did it work** — a line `재생목록 N개 · M곡 · …` (N playlists · M tracks · …) appears and the lists show in My playlists.

- Choosing the whole folder gives tracks their names. With only the playlist files they show as `이름 모르는 항목` (unnamed item).
- Importing the same list again replaces it. **Delete…** removes only the list imported into Fidenne.

## 5. Listening History page

Where you see what you listened to on this Mac. Nothing is uploaded automatically; you can only export it yourself.

- **What counts as one play** — while Fidenne is open, 30 seconds of actual playback or half the track (whichever is shorter). Nothing is recorded while the app is closed.
- **Entries removed from Home** — a song hidden with **Remove from History** on the music home page is still counted in this page's statistics. To remove it from statistics too, use **Delete listening history** below.
- **Local files** — only the tags (title · artist · album) are kept; file paths · folder names · file names are not.
- **Export** — JSON · CSV (the chosen source only). **Delete** — **Delete listening history (청취 기록 지우기)** in the fold **History settings and counting rules (기록 설정과 집계 기준)** → **Delete all (모두 지우기)**. This cannot be undone. Turning off **Keep listening history on this Mac (이 Mac에 청취 기록 저장)** stops recording.
- Genre · BPM use only what the playback app gives. Missing values are not guessed.
- **Spotify-provided lists (Spotify 에서 제공한 목록)** — switch the tab to see Spotify's own top tracks · top artists (period **4 weeks · 6 months · 1 year**) and recently played, as Spotify gives them. You must be connected with your own Client ID; Fidenne computes no counts · shares · genres from this list and discards it when you leave the screen. The order is not play-count order. Pressing a row opens that track in Spotify (**OPEN SPOTIFY**).

<a id="6-dsp-page"></a>
## 6. DSP pages

Choose a page such as **EQ**, **Ostrum** or **Crossfeed** in the sidebar’s **DSP** group. The input rate is shown in the header (the last playback rate while stopped). The Response graph is above the controls; open **Advanced** to edit individual bands.

- **Changes are heard at once; save (⌘S) to keep them for the next launch.** The same for EQ and Ostrum. Edits stay when you visit another page and come back.
- Button and field names are in English, notices and warnings in Korean. DSP is heard only on outputs Fidenne processes (DSD · PCM oversampling); PCM Direct does not pass through it.

### 6.1 Response graph

The lines are **Target (타깃)** (orange dashes, the goal) · **My headphone (내 헤드폰)** (grey, the measurement) · **After correction (보정 뒤)** (the darkest line = my headphone + EQ + Ostrum) · **EQ curve (EQ 곡선)** (blue; the band points sit on it), and the **More (더 보기)** menu has EQ + Ostrum · Ostrum. Fitting the EQ means bringing **After correction** onto **Target**.

- Turn lines on and off in the legend under the graph. **View** in the card header chooses **Original** / **Target flat** (target drawn as the 0 dB line).
- Curves are drawn without the EQ Preamp and Ostrum's Headroom · Output (to compare shapes). The sound still has them, and the first line of the fold **How to read the graph · notes (그래프 읽는 법 · 주석)** gives the values.
- The EQ + Ostrum line is the EQ (engine calculation, left channel) plus the size of Ostrum's centre sound. Crossfeed does not change the centre, so it is not included.
- It draws without playback too (when stopped, at the last playback rate). **Reference** (1 kHz etc.) · **Range** (auto · ±12 · ±18 · ±24 dB) in the card header change only the picture, not the sound.
- **Spectrum** — the current sound's level per band lies faintly behind the graph. The **Spectrum** line under the legend chooses **After DSP (DSP 뒤)** · **Both (앞뒤 겹쳐)** · **Before DSP (DSP 앞)**, resolution · smoothing · peak hold. It moves only during playback.
- **Excess-setting detector** (one line under the graph) — when the sum of EQ · Ostrum · Crossfeed boosts too much (over +6.2 dB), goes over 0 dB or is too steep, it draws red regions on the graph. It does not block anything.
  - A correction that changes bands happens only when you press **Apply fix (보정 적용)** in **Suggest a fix… (보정 제안…)**. The window opens on **Industry practice (업계 관례)** (lower the Preamp only); **Improved (개선)** (the smallest change to the bands that make the overflowing boost or steep slope) is used only when you pick it (it opens on Improved when industry practice cannot remove what was found). See the table of bands that change and press **Apply fix (보정 적용)** to change them. Improved trims the curve, so the sound may differ from what you wanted. **Undo fix (보정 되돌리기)** goes back once.
  - The only automatic part is **Prevent clipping — lower Preamp automatically (클리핑 막기 — Preamp 자동 낮춤)** (off by default). When on, it lowers only the Preamp as much as needed when the sum goes over 0 dB, and never changes a band.

### 6.2 Equalizer

Use **Turn on EQ** at the top of the EQ page. Choose saved settings in **My EQ**, or headphones and a target in **AutoEQ**. The save row contains **Revert to saved**, **Reset** and **Save** (⌘S).

1. Change bands by dragging a graph point or with a slider · number field in the band columns. It is heard at once.
2. When you like it, press **Save** (⌘S).

**Did it work** — the line under the header reads `✓ 저장됨 · 다음 실행에도 이 EQ 로 시작합니다` (saved · the next launch starts with this EQ). Before saving it is the orange `● 저장 안 됨 — 저장(⌘S)해야 다음 실행에도 남습니다` (not saved).

- **Presets ▾** — keep a named EQ and choose it again.
  - The **recent** five and **All presets**. Choosing one is heard at once and the next launch starts with that EQ. The headphone · target the preset was fitted to and its strength come into the Auto EQ row with it, and **Bands** becomes that EQ's band count (100 % for a preset kept without a strength).
  - With a preset chosen, saving (⌘S) also overwrites **that preset** with the EQ and the headphone · target. Changing only the headphone · target also turns Save on.
  - **Save as… (다른 이름으로 저장…)** saves the current EQ and keeps it under a new name (the current preset is untouched; up to 100). **Manage presets… (프리셋 관리…)** renames · deletes, and **Back to an earlier save (이전 저장본으로 되돌리기)** holds the EQ that was there before each save (the last 20).
- **Back to saved** returns to the last saved EQ, **Reset** sets all bands and the Preamp to 0 dB (flat). Both are heard at once.
- Quitting with an unsaved EQ playing asks once — save and quit · quit without saving · cancel.
- **Band columns** — **Preamp** first, then per band an on box and number · gain slider · type (PK · LS · HS · LP · HP · BP · NO · AP · G) · channel (L+R · L · R) · Gain · Freq · Q fields. Above the columns: **Open EQ preset… (EQ 프리셋 열기…)** · **31-band graphic (31밴드 그래픽)** · **Add band (밴드 추가)** · **Delete band (밴드 삭제)** · **Reset band (밴드 초기화)**. Up to 32 bands; **Open EQ preset… (EQ 프리셋 열기…)** opens AutoEq · Equalizer APO files.
- **Import into My EQ** — read a Room EQ Wizard (REW) filter-settings file, an Equalizer APO config or an AutoEq Parametric text file (.txt, up to 2 MB) as a new EQ. In the EQ panel of Playback Chain press **Import… (가져오기…)** under **My EQ (내 EQ)**, or drop the file on the EQ settings area. You first see **Imported (가져온 것)** (band count · preamp) and **Not imported (가져오지 않은 것)** (filter types this EQ does not have · values out of range · filters written without a Q · filters beyond 32 bands · Include · conditional sections · channel selectors, each with its reason). Values are never shrunk or changed; such filters are skipped, and if any line cannot be read the whole file is refused and the line number is given. Name it and press **Save to My EQ (내 EQ에 저장)**; it only saves — the sound does not change until you choose it in **My EQ**. A GraphicEQ curve is not a set of filters and is not saved here (use **Open EQ preset… (EQ 프리셋 열기…)** above to fit filters to a curve).
- **How EQ is calculated** — the EQ filter coefficients are computed to match their analog prototypes (matched). Before, the curve bent near Nyquist (half the output rate); now at high frequencies (especially above 16 kHz) the curve you set follows the real curve more closely. An EQ with filters in the treble can sound slightly different with the same settings. The engine processes at the output rate, so at 352.8 kHz and in DSD the difference is tiny (0.002 dB or less on test signals) and it is clearer at low rates such as 44.1 · 48 kHz. It was not checked by ear.
- **Clipping & Headroom** (under the band columns) — whether this playback clipped, the limiter, and the **Apply Headroom N dB** suggestion button.
- **EQ method** — **Parametric** (default, no delay) / **Minimum-phase FIR** / **Linear-phase FIR** (about 0.2 s delay, from the next playback start). With linear phase, **Linear Phase length** chooses the length. Which sounds better has never been checked.
- If the engine cannot build the EQ at that rate, an orange line says so and it plays without EQ (the saved EQ stays). Right after turning EQ off it may sound a little quieter for 0.1–0.3 s before coming up — this prevents a loud jump.

### 6.3 Ostrum

Fidenne's tone shaper for bass · presence · width · harmonics together. Knobs are heard as you move them; to keep them, press **Save** (⌘S) in the header.

1. Turn on **Ostrum On**.
2. Choose a starting point from **Presets ▾**, or press **Start natural (자연스럽게 시작)**, which appears while **Mix** is 0.
3. Move the knobs a little at a time while listening, and save when you like it.

**Did it work** — the panel's top line reads "적용됨 · 리비전 N" (applied · revision N) and the Composite Response graph changes.

**Presets ▾** — starting points **Natural (자연스럽게)** (lightest, recommended first) · **Clear OST · vocals (선명한 OST·보컬)** · **Bass-focused · electronic (저음 중심·전자음악)** · **Night · less fatigue (야간·피로 적게)** (weakest). These are suggestions, not values settled by listening. **Save current settings as my preset… (지금 설정을 내 프리셋으로 저장…)** keeps your own, and the same menu chooses · renames · deletes them.

| Knob · field | What it does |
|---|---|
| **Mix** | The overall amount. At 0, Bass · Presence are not heard. Raise it first |
| **Bass** | Sound · Compression · Tune. **Split Bass** treats deep bass and the low range above it separately. **Topology** is Blend (default) / Manual [Experimental] |
| **Presence** | How much the treble is raised (Intensity) and how (Off · Analog · Min Phase · Linear Phase). Linear Phase from the next playback, or **Restart Now** |
| **Width** | The size of the left–right difference |
| **Harmonics** | Adds harmonics (Curve · Amount) |
| **Headroom · Output** | The overall level. When **Recommended Headroom** appears, press **Set Headroom to the recommended value (권장값으로 Headroom 맞추기)**. Turning on **Automatically on every change (바뀔 때마다 자동으로)** beside it (off by default) makes the knob follow the recommendation |

- **Tune** is Presence's reference frequency. To raise Mix, keep Tune within 1.1–22 kHz; otherwise an orange line beside the knobs says so (when the engine refuses a setting it also says why and what to change, in one sentence). The Tune knob has the low Hz on the left.
- **Neutral Tune** leaves out Bass · Presence and uses only Width · Harmonics · Output. **ⓘ** beside each item gives when to use it and the cost.
- While the Bass compression is pressing down, the graph shows a faint purple hatching and `압축 중 −x dB` (compressing −x dB).

### 6.4 Crossfeed

When left and right sound too far apart on headphones, it mixes in a little of the other side.

1. Turn on **Turn on crossfeed (크로스피드 켜기)**.
2. Choose one of **Light · Normal · Strong (가볍게 · 보통 · 진하게)** (least mixing first).
3. To refine it, turn the two knobs — **Amount (Feed)** is how much is mixed (−15 … −1 dB, more toward −1), **Frequency (Cutoff)** is up to what pitch (300–2,000 Hz).

**Did it work** — the chosen button stays pressed, and in the small M/S graph (during playback) the Side line drops.

- The **My settings (내 설정)** menu saves · loads · deletes the current values by name (up to twenty). **ⓘ** under the knobs says which way to turn when the sound feels stuck inside your head · when left and right feel too narrow.
- Turned on together with Ostrum's Width, "폭을 두 곳에서 조절 중" (width adjusted in two places) appears. The two partly cancel each other in the same band.

### 6.5 Headphone ▾ · Target ▾ (the Auto EQ row of Equalizer) · Advanced — files · treble · Generative AI (collapsible)
<a id="65-headphone---target--the-auto-eq-row-of-equalizer--advanced--files--treble--llm-collapsible"></a>

Where an EQ is made automatically to fit a headphone measurement. Press the **Auto EQ row** in front of the band columns inside Equalizer to open it.

At the top of the DSP page's EQ section, **My EQ** (pick a saved EQ) and **AutoEQ** (my headphone, target, bands, apply) sit one above the other, and the one in use is marked. Choosing something in the other one moves the mark to it. Below them are **EQ method** (parametric, minimum phase, linear phase) and the save row; more detailed settings are further down under **Advanced**.

1. Choose your headphone in **My headphones (내 헤드폰)**. If it is not listed, **Search headphones… (헤드폰 검색…)**.
2. Choose the goal in **Target (목표)** — the measurer's target curve (DF · DF t · Harman …) or another headphone.
3. Press **Apply (적용)** at the row's end ([§6.6](#66-bands--strength--auto-fit-the-auto-eq-row-of-equalizer--what-auto-fit-did-collapsible)).

**Did it work** — the folded row reads like `Auto EQ   my headphone → goal · 10 bands`.

- Choosing a headphone · goal does not change the EQ. It changes when you press Auto fit.
- **Search headphones…** — downloads squig.link's measurement list and searches it on this Mac (the query is not sent). Press **Get list (목록 받기)** the first time; a received list is not downloaded again for 30 days. If a list saved by an earlier version lacks the in-ear measurement lists, only the missing ones are downloaded in the background when you open it (only while squig.link is switched on). **Download the list again from the measurement sites** downloads everything again at any time. Pressing a row opens a check box, and it changes only when you press **Apply (적용)** (Return). **☆** marks a favourite (my headphones · target headphones are kept apart).
- **Target search** — the AutoEQ **Target** list on the DSP page has a search field. Typing shows up to 12 headphones from the measurement list (the headphone of mine on show is left out), and pressing a row aims at that headphone. Search results · favourite targets · favourite my-headphones carry an always-visible **☆ / ★** at the end of the row to add or remove a favourite. Removing a favourite never changes the target you have chosen. If the measurement list has not been downloaded yet, a line tells you to download it first. The Target list in the Playback Chain panel is unchanged and its last row leads to the DSP page.
- If my headphone and the goal were measured on different rigs, the status line says so and **Rig difference correction (측정기 차이 보정)** (on by default) adjusts it. Goals whose rig relation cannot be known are hidden from the list. A goal of another kind (a headphone with an earphone target, for example) gets a yellow line and is not blocked.
- **Advanced — files · treble · Generative AI** (fold):
  - **Open from file** — **Open measurement…** · **Open target…** open your own measurement · target file (two-column Hz · dB text).
  - **Treble (Auto fit)** — how far to correct the treble (all · none above the boundary · half above 6–8 kHz etc.). Applied when you press Auto fit.
  - **Refine with generative AI (생성형 AI로 다듬기)** — **Copy text for the AI (AI에 줄 글 복사)** or export a file, refine it in the generative AI you use (ChatGPT · Claude etc.), paste the answer and press **Import the pasted answer (붙여 넣은 답 가져오기)**. The app sends nothing.

### 6.6 Bands · Strength · Auto fit (the Auto EQ row of Equalizer) · What auto fit did (collapsible)

- **Bands** — the number of bands. AutoEQ offers **10 · 16**, while Advanced offers **5 · 10 · 15 · 32** and **Other** (1–32). 10 is the default. If a narrow wiggle remains at 4–8 kHz after fitting, raise it to 12–16 and fit again.
- **Strength** — correction strength (0–100 %, default 100 %). Lowering it scales every band's gain by the same ratio.
- **Apply (적용)** — the fitted bands go into the band columns and are **heard at once**. Save (⌘S) to keep them. If it cannot fit, the button is off and the reason shows in orange.
- **What auto fit did (자동 맞춤이 한 일)** (fold) — one sentence per band (for example "3 kHz 부근 4.0 dB 줄임 — 중고역 …", cut 4.0 dB near 3 kHz — upper mids …) and the error figures. It is not a judgment that the sound is good.
- With Ostrum on, Auto fit fits only the EQ, so the **After correction** line may look off the target.

### 6.7 The A/B button's panel — A/B · ABX · Auto Bypass · Loop · Level-matched Comparison (음량 맞춤)

A/B · ABX · Auto Bypass · Loop comparison is **hidden in this beta** — the DSP page shows no A/B button. It comes back once it is fixed ([Known limitations](KNOWN_LIMITATIONS.md)).

### 6.8 Convolution (IR) page

Open **Convolution (컨볼루션)** in the sidebar's **DSP** group to apply an IR (impulse response) file to music. You can use a correction IR or a four-channel BRIR.

- **Choose IR File… (IR 파일 고르기…)** — WAV or AIFF (AIFC), 1 · 2 · 4 channels, 44.1–192 kHz, up to 1,048,576 samples per channel, 16/24/32-bit integer or 32/64-bit float. No IRs are included. Choose a file you measured yourself or have the right to use.
- Mono uses the same IR on both sides, stereo uses separate left and right IRs, and four channels are true stereo. For a four-channel file, check **Channel order (채널 순서)** against the file: **LL · LR · RL · RR (default)** or **LL · RL · LR · RR**.
- Picking a new file requests **the lower of the current gain and that file's suggested gain**, and shows the value in the gain field. Picking the first file does not turn it on. Use **Turn On (켜기)** to turn it on or off.
- After editing **Gain (게인)**, press **Apply (적용)** or Return. **Suggested value (제안값)** applies the suggested gain immediately. **Response peak · suggested gain · gain ceiling** come from the engine. The ceiling uses **the full response from 0 Hz through Nyquist plus a 1 dB margin**, beyond the display graph's range. The suggestion leaves 0.2 dB of headroom against that response bound. The IR itself is not automatically normalized.
- While the IR is actually being applied, **Compare without the IR, at the same latency (IR 없이 같은 지연으로 비교)** removes just the IR for comparison. Convolution is the last PCM processing stage, after EQ · Ostrum · crossfeed and before the modulator. The IR is converted to the engine rate if needed. Turning it on adds about 24–49 ms of latency; check the panel for actual latency and processing state.

### 6.9 Plug-in page

On the **Plug-in (플러그인)** page in the sidebar's **DSP** group, put Audio Unit (AU) effect plug-ins in the path the sound takes. Changes are heard from the next playback; when off, the sound passes through unchanged.

1. Press **Add Plug-in (플러그인 추가)**; the effect plug-ins installed on this Mac are listed by maker. Choose one. A plug-in seen for the first time, or whose version changed, is first checked by Fidenne with macOS's validation tool (auval) (`Checked n of m plug-ins`), and only plug-ins that pass can be used.
2. Turn the card on with **Turn On (켜기)**. There are **at most 4 slots**; the page header shows how many are used (for example 2/4).
3. Optional: **Open Editor (편집기 열기)** opens the plug-in's own screen in a separate window (a plug-in without one says `This plug-in has no screen of its own`).

- **Positions** — a plug-in sits in one of three places: **Before EQ · Ostrum** · **Between EQ · Ostrum and Crossfeed** · **After Crossfeed**. On the page, Fidenne's own EQ · Ostrum and Crossfeed appear as thin lines between the positions (fixed; not switched here). Within one position they run from top to bottom; drag ≡ or press ⌥↑ · ⌥↓ to reorder — the order the sound passes through changes too. The card's menu does the same.
- **Remove (빼기)** asks once when settings are saved.
- **Notices** — if a plug-in cannot be used as stereo, does not accept the track's sample rate, cannot keep up, has too large a delay, produces invalid sound or makes the sound too loud, Fidenne turns it off and writes the reason on the card. **Turn Back On (다시 켜기)** or **Reload (다시 불러오기)** brings it back. The settings of a plug-in that is not installed are kept. If the saved list cannot be read, the list is left unchanged.
- Plug-ins run in a separate process outside Fidenne, and the sound being played is passed to them. Their behavior follows their maker's terms. They run on outputs Fidenne processes, and their settings are saved and restored at the next launch.
- Only a test plug-in was checked; not every plug-in on the market ([Known limitations](KNOWN_LIMITATIONS.md)).

**How to tell it worked** — during playback the card shows `Working · Delay ○ ms`, and the plug-in chip in Playback Chain is on.

## 7. I/O · Diagnostics Page

### 7.1 Independent output control · Output mode

Choose one of three in **Output method (출력 방식)** at the top of the page (**PCM Direct** · **PCM oversampling (PCM 오버샘플)** · **DSD**). A line on each card says what the sound passes through, and a **Settings used (쓰는 설정)** line says which settings that mode reads. The detailed values (filter · DSD conversion · PCM · headroom) are in the **Advanced (고급)** fold; a row the current mode does not use stays greyed and keeps its saved values.

- **PCM Direct** — Fidenne does not process the sound. It goes playback app → macOS → DAC as is. The sample rate is not matched track by track (because the sound does not pass through Fidenne, it cannot change the output rate to the track's (input) rate): when the DAC's rate and the track's differ, macOS converts. The DAC's rate is set once at start (44.1 kHz for Spotify; if the DAC was left at a rate that is not ordinary PCM, such as DSD or 352.8 kHz, the track's rate, or 44.1 kHz when unknown).
- **PCM oversampling** — Fidenne raises the sound with a filter and sends integer PCM (it is not turned into 1-bit DSD). The output rate, bit depth and dither are set in **Advanced › PCM** (below).
- **DSD (DoP)** — Fidenne sends DSD through filter → DSD modulator → DoP.
- **Built-in speakers · AirPods · 3.5 mm · HDMI** — Fidenne processes the sound and sends it; macOS mixes the result through its system mixer before sending it to the device. The DSD card is greyed out and only PCM is sent ("DSD output is limited on this device"). A stored DSD choice is kept and used again when you are back on a DAC. The status line and the device line also describe the PCM that really goes out (via the system mixer). A control that cannot be changed while playing shows the reason in one line.
- With EQ · Ostrum · Crossfeed off there is no tone-changing processing in PCM oversampling or DSD. The conversions the format needs (upsampling filter · DSD modulator · dither · headroom) still run, and the character of the sound may vary with the filter and modulator you choose.
- **Sound presets** — drag a card in **My presets (내 프리셋)** to change the order (a card's menu also moves it earlier or later). The eye at the end of the **Recommended (추천)** line hides the recommendation cards; the eye in the same place shows them again. The recommended order never changes.
- In PCM Direct, local files keep the source rate, bypass sound processing and disable dither.
- Check the DAC volume before switching to PCM Direct — Fidenne's headroom does not apply, so it may sound louder.
- **Playing sound is not touched.** When a track moves on to the next one by itself, PCM Direct does not stop, rewind or change the DAC rate. If the rates differ it keeps the current rate and macOS converts, so nothing is cut. Matching the rate to a track happens only when you pick the track yourself, before any sound. Pause · resume · seek do not change the rate either. The rate learned for each track is remembered by service and by evidence (track · album) and used the next time you pick it yourself. An album with a different release counts as a different memory, and when the exact release is unknown nothing is guessed.

The chosen output mode stays for the next launch. DSD · PCM oversampling are restored only if that format was confirmed on that DAC before; otherwise it **starts in PCM Direct** and says so in one line. Opening the app alone never starts sound.

**Advanced › PCM — output rate · between songs** (used by PCM oversampling; local files in PCM Direct keep the source rate, bypass processing and disable dither)

- **Output rate (출력 레이트)** — 44.1 · 48 · 88.2 · 96 · 176.4 · 192 · 352.8 · 384 · 705.6 · 768 kHz. A new configuration keeps the source rate. A rate the device does not take stays in the list greyed with `This device doesn’t accept it`. If the chosen rate is not taken, a button (for example **Change to 192 kHz**) goes to the highest rate the device takes. At low rates, if the 24-bit noise margin falls short of the reference, a line says so.
- **Follow the source's rate family (음원 계열 따라가기)** — off by default. On, a song in the 44.1 kHz family (44.1 · 88.2 · 176.4 …) goes out in the 44.1 family and a song in the 48 kHz family (48 · 96 · 192 …) in the 48 family. The popup becomes multiplier rows (for example `88.2 / 96 kHz (×2)`), and its first row **Auto (highest the device takes) (자동(장치 최고))** picks the highest multiple the device takes in the song's family, with the result beside it (`Auto → 384 kHz`); it is not the default. It goes briefly quiet between songs that change family. If the song's rate is not known yet or is only a guess, the family is not changed (`Source rate not confirmed yet — keeping the current family`). If the device does not take the family, it converts to the other family and says so once. The rate changes only between songs, never mid-song, and sound received through the system tap follows the format at session start.
- **Read line** — what the engine actually did, as `Source 44.1 kHz → output 176.4 kHz (×4) · 24-bit`; where the output is not the source times a power of two, the brackets say `downsampled` or `converted`. The limiter is not available at ×1 or downsampling (`The limiter is not available at this multiple (×1 or downsampling)`), and below 88.2 kHz the ultrasonic check reads `not applicable`. At low output rates, whether the sound is nearing full scale is judged by true peak.
- **Between songs (곡 사이)** — **Unchanged (그대로)** (default: leaves the music untouched and joins songs with digital silence) or **Smooth (부드럽게)** (fades the last 0.02 s of a song). Choosing restarts nothing; it applies from the next song. Each song shows a line such as `This song: Unchanged · the rate changed, so 250 ms of silence comes first`. This applies when playing a local file as PCM; for streaming sound that Fidenne receives and processes, and for DSD, nothing changes (the line is not shown).
- **Wait when the rate changes (레이트를 바꿀 때 기다림)** — set per DAC: **Off (꺼짐)** · **0.25 s** (default) · **0.5 s** · **1 s** · **2 s**. Make it longer if the first sound is cut off while the DAC locks to the new rate. It cannot be set until an output device is chosen.
- **Bit depth** (24 · 16-bit) · **Dither** — as before.

**Built-in speakers · 3.5 mm jack · AirPods (Bluetooth) · HDMI · DisplayPort · AirPlay**

- Fidenne processes EQ · Ostrum · crossfeed · filters and the engine PCM output and sends the result to these devices too. macOS mixes the result through its **system mixer** before sending it to the device, so it is not bit-perfect; the read line says `via system mixer · not bit-perfect`. The output is PCM Float32; bit depth and dither cannot be chosen (greyed), and neither can the output rate — the engine processes at the highest supported rate from 44.1 to 768 kHz that is at or below the device's current rate (48 kHz for a 48 kHz device) and macOS converts once to the device rate if needed. The read line may show `Device ○ kHz · macOS converts once (highest quality)` and a Bluetooth delay.
- Fidenne does not write these devices' rate, so **Wait when the rate changes** reads not applicable. If another app changes the device rate, it restarts once at that rate, and a local file that was playing stops (`Click Play again`). When a Bluetooth device goes into its call mode (a microphone app is using it), Fidenne pauses its processing and starts again by itself when that app closes.
- Volume is the Mac's volume — on a device used for the first time, `Turn the Mac volume down to 0 or very low before starting, then raise it slowly while you listen.` appears.
- Fidenne processes the sound on this path and sends it; macOS mixes the result through its system mixer before sending it to the device, so it is not bit-perfect. Checking on real speakers · AirPods · monitors was partial in this version ([Known limitations](KNOWN_LIMITATIONS.md)).

- **Output DAC** — choose · refresh · reconnect. Devices that take none of the engine's PCM rates (44.1 to 768 kHz), or have no 2-channel format (most dongles · 4- and 8-channel interfaces · some monitors), get `· PCM Direct only` after the name; DSP and library playback do not work on them and they play only in PCM Direct. Fidenne processes the sound and sends it to built-in speakers · AirPods · HDMI too, so they do not get this mark; macOS mixes the result through its system mixer before sending it to the device. A USB DAC plugged into another port is still recognised; when unsure it asks once: **Use as the same device (같은 장치로 쓰기)** / **Use as a different device (다른 장치로 쓰기)**.

### 7.2 DAC format check (formerly "Engine output format")

A table of which formats your DAC takes (DSD128 · DSD256 · PCM 24 · 16-bit). Each shows **Confirmed (확인됨)** (✓) · **Refused by the engine (엔진이 거절함)** (⚠ + reason) · **Not yet checked** · **Unknown (모름)**, remembered per DAC.

- **Check all (모두 확인)** — pressed while stopped, it tries each unchecked format in turn and restores the original. No sound plays, but the DAC may click or its display may change briefly.
- If the DAC does not take the chosen format, Fidenne does not drop to another rate; it does not start.
- **It asks once the first time it sends DoP** — `<DAC 이름>로 DSD(DoP)를 처음 보냅니다` (sending DSD (DoP) to <DAC> for the first time). Confirmed in the table does not mean the DAC decodes DoP; a DAC that cannot plays loud noise.
  Lower the volume or take off the headphones; if the DAC's manual lists DoP press **DoP를 받는 DAC · 시작** (DAC takes DoP · start), otherwise **PCM 24-bit로 재생** (play as PCM 24-bit). Check that the DAC's indicator shows DSD; if you chose wrongly, **Ask again (다시 묻기)** on the DoP line under the table.
- With a DAC whose volume control is linked to the macOS volume, Fidenne takes that volume over for DSD · integer PCM output: it plays at the same loudness by lowering the sound inside Fidenne, and gives the volume back afterwards. The output device line in Playback Chain shows `DAC 음량 −○ dB 를 Fidenne 이 넘겨받음` (Fidenne took over the DAC volume of −○ dB). If it cannot, you see `이 DAC 의 음량을 Fidenne 이 넘겨받지 못했습니다` (Fidenne could not take over this DAC's volume) — listen to that DAC with PCM Direct ([Troubleshooting](TROUBLESHOOTING.md#dac-volume-and-dsd-dop--integer-pcm)).
- **If the DAC reconnects within N seconds, resume (DAC가 N초 안에 다시 연결되면 이어서 재생)** — waits for the same DAC only. "Don't wait (기다리지 않기)" turns it off.
- **Output after quit (끈 뒤 출력)** — under I/O › Advanced. On quit, Fidenne returns to the device used before launch if it is available. Otherwise **Last DAC** (default) tries the last external output device, excluding the Mac’s built-in speakers and headphone jack; **Mac speakers** selects the speakers. Missing external devices fall back to the Mac speakers. Returning to the Mac speakers lowers their volume to the minimum first. External DAC volume is unchanged, so the next playback can be loud if it was left high. This setting is editable during playback.
- It starts even if another app is using the DAC. If that app does not let go, `다른 앱(…)이 DAC에서 물러나지 않아…` (another app did not move away from the DAC…) shows once and it does not retry. Meanwhile the other app's sound may move to the Mac speakers.
- If `DAC 재생 통로가 macOS 안에서 멈췄습니다…` (the DAC playback path stopped inside macOS…) appears, unplug and replug the USB cable or restart Fidenne ([Troubleshooting Guide](TROUBLESHOOTING.md)).

### 7.3 Streaming-app autoplay · Input and output devices

**After the engine starts (엔진 시작 후)** — what to do when the engine turns on. **Auto-detect (자동 감지)** starts no track and follows the app that is playing (for browser sound, keep this and play in the browser). **Apple Music** · **Spotify** play that app's current item, **YouTube Music (browser)** sends ▶ to the open tab. **No autoplay (자동재생 안 함)** only turns the engine on. When Music and Spotify play at once, Fidenne follows the one started last and pauses the other.

**Input** — how the sound is received. The chosen input carries over to the next launch.

- **Fidenne Inlet** (recommended) — receives the playback app's source rate as is. **Install… / Update… / Remove… (설치… / 업데이트… / 제거…)** in the same box. When a newer version is available, the home screen tells you while nothing is playing. Installing · removing asks for the administrator password and briefly silences all apps — do it when you are not listening. Alert sounds do not go to Fidenne Inlet. If the device's rate is changed during playback, it goes quiet for 1–3 s and continues at the new rate. If "옛 이름으로 설치되어 있습니다" (installed under the old name) shows, install again (your choice of input stays).
- **System tap (시스템 탭)** (listed as **Process Tap**) — receives all apps' sound on this Mac at 48 kHz without installing. While receiving, that sound plays only through Fidenne, and turning the engine off returns it at once. macOS asks for audio recording permission on first use — if declined it is silent (System Settings › Privacy & Security › Screen & System Audio Recording). To receive only one app's sound, send that app's output to Fidenne Inlet and choose Fidenne Inlet as the input.
- **+ Other input device (+ 다른 입력 장치)** — picks another loopback device you already use (only devices with both an output and a 2-channel input; remove with **✕**).

**Apple Music source rate** — the input rate follows each Apple Music track's source rate. Fidenne remembers on this Mac the rate of tracks you played, so next time they start at the right rate. For a track heard for the first time, the first sound is held briefly (usually under 1 s, at most 2 s) until the rate is known. Spotify does not report its source rate, so it is set to 44.1 kHz.

### 7.4 Filter · Modulator · Output gain (card) — sound settings for the DSD path

The sound settings are in **I/O · Diagnostics › Advanced**. Open **Filter**, **DSD conversion**, **PCM**, **Headroom** or **Buffer** separately. Recommendations and **Save Current Settings as a Preset…** are in the **Sound presets** card.

The **Recommended combinations N (추천 조합 N개)** fold in the **Where shall we start listening? (어디서부터 들어볼까요?)** card holds recommendations by purpose. Each card says what to listen for, and changes only what it lists. Choosing one during playback pauses briefly and continues.

1. **Filter** — processing type (standard SRC · long-tap extension · ultra-long-tap) · family · length. A filter with an [Experimental] badge states its caveat. Long and ultra-long filters delay the sound, so they show **delay ○○ ms** as a warning that video may drift — for video, standard SRC and the **Low latency (저지연)** buffer drift least. The fold **Choose by conditions · compare costs (조건으로 고르기 · 비용 비교)** filters by maximum delay · CPU. The 20 Hz–18 kHz response is practically the same for all filters; what differs is above 20 kHz and the time response. The long-tap extension also has **Cardinal Sinc 128K** and **Cardinal Sinc 64K**, each with a **Follow (따라감)** twin whose cutoff follows the source rate (on 44.1 and 48 kHz songs the twin sounds the same). They are fixed-length sinc filters with the delays shown in the list (128K about 116 ms, 64K about 70 ms for the 44.1 kHz family). They were checked with automatic tests and measurements, not by comparing them by ear.
2. **DSD conversion** — the **conversion method (변환 방식)** is **Safe (안전)** (5th order, light) / **Precise (정밀, default)** (7th order · recommended) / **CLANS** (experimental) / **Trellis** (experimental · heavy), with output rate DSD128 / DSD256. DSD256 becomes the default once confirmed on that DAC. **CLANS** is a new experimental conversion method in 0.7.0: a fixed 7th-order modulator with the same protection as Precise. It is available only at DSD128 and DSD256 of the 44.1 kHz family, is not used with dither, and choosing it shows "CLANS is still being tested. If the sound breaks up or seems wrong, switch back to ‘Precise’." Trellis is still being tested: it looks ahead when choosing each bit, adds a 7-bit delay, and is not used together with the experimental dither. Choosing it shows "Trellis is still being tested — if sound breaks up or seems off, switch back to Precise." If the sound breaks up the same notice appears once more, but the method is never switched for you. If this Mac cannot finish the Trellis calculation in time, playback stops and the notice "Trellis processing did not finish in time on this Mac, so playback was stopped. Using ‘Precise’, ‘Safe’ or the CLANS modulator lowers the load." appears with a **Choose conversion method (변환 방식 고르기)** button, which brings you back to this choice. Precise stays the default and nothing changes until you pick Trellis yourself.
   - **Buffer (버퍼)** — low latency · standard · **stable (default)**. Sound quality is the same; only how soon a change is heard and how well it resists dropouts differ. Change it while stopped; it applies from the next playback.
   - **Dither** — available for Safe. New seventh-order dither selection is hidden in the distribution; a previously enabled setting can be turned off. CLANS and Trellis do not use dither.
3. **PCM headroom (PCM 헤드룸)** — **Auto (recommended) (자동 (권장))** is the default. It lowers the whole signal by what EQ · Ostrum raised, to prevent clipping. Changing it with the slider · buttons makes it **manual**, and **Back to auto (자동으로 되돌리기)** returns. It is auto again after relaunch. It is not the DAC volume — set the listening level on the DAC.

- **Save current sound preset (현재 사운드 프리셋 저장)** — saves ① filter · ② DSD conversion (with experimental dither) · ③ headroom as one preset. Saved presets can also be chosen from the output mode menu in the bottom bar.
- **Current selection guide (현재 선택 가이드)** — what the chosen filter changes, where to listen, what it costs, and its frequency response graph.
- If the Precise modulator needed stabilising, it shows the count and suggests "Switch to Safe" · "Switch to DSD256".

### 7.5 Playback Chain · Actual behavior · Diagnostics

- **Playback Chain** card — the same as in the window header ([§2.1](#21-page-header)). If "출력은 안전하게 정지했습니다." (output stopped safely) appears, press **Reconnect DAC (DAC 다시 연결)**.
- **Actual behavior · diagnostics (실제 동작 · 진단)** (fold) — requested and actual rate, remaining headroom, estimated output delay, dropped-sound · underrun counts. The delay is a software estimate, not a measurement of the DAC's analogue output.

## 8. Settings Window

Open it with **⌘,** · **Settings… (설정…)** in the app menu · the **Settings…** row at the bottom of the sidebar. Changes apply at once and stay for the next launch.

**Screen language** — Korean · English · Japanese screens are included. There is no language switch inside the app; it follows macOS's language order (System Settings › General › Language & Region). If none of the three is first, it is Korean. The English and Japanese sentences are AI drafts and have not been reviewed by a native speaker; please tell us about awkward ones.

- **General (일반)** — **YouTube Music (experimental) (YouTube Music (실험 기능))** (when off it does not appear in the service list, the playback capsule, the Lyrics tab chips or the YouTube Music box under Privacy; off on a fresh install) · version and **Check for updates…** · **Interface scale (인터페이스 배율)** (also stepped one size at a time from the View menu: **Zoom In** ⌘+ / ⌘=, **Zoom Out** ⌘−, **Actual Size** ⌘0, with the new size shown briefly in the middle of the window) · **Grow automatically in a large window (큰 창에서 자동으로 키우기)** (on by default — when the window is larger than 1440×900 the whole screen, text, sidebar, playback capsule and buttons included, grows together up to 1.5 times, and `지금 N%` (now N%) shows while it is on. When off, only the interface scale applies) · **Theme (테마)** (system / light / dark; dark on a fresh install; light is not a finished theme yet) · **Liquid Glass** (below macOS 26 a note says `이 macOS에서는 반투명 효과로 대신 그립니다.` — translucent materials are drawn instead; its ⓘ explains that windows use macOS's translucent material) · **Playback capsule (재생 캡슐)** (material · transparency — below macOS 26 the capsule is always opaque so it stands apart from the window behind it, the **material (재질)** picker is not shown, and your chosen material applies again on macOS 26 or later) · **Motion effects (동작 효과)** · **Restore display defaults (화면 설정 기본값 복원)** · **Help (도움말)** (diagnostics for problem reports, [§10](#10-sending-a-support-file)).
- **Controls and shortcuts (조작과 단축키)** — two-finger scrolling · trackpad haptics · **Show controls** · **Show tips again** · the shortcut list ([§2.4](#24-menu-bar-icon--menus)).
- **Sound safety (소리 안전)** — **Volume notice at every start (켤 때마다 음량 안내)** (on by default) · **Mute when a signal not found in music appears (음악에 없는 신호가 나오면 음소거)** (on by default). See [§1](#1-first-launch--the-five-step-first-run-setup).
- **Privacy (개인정보)**
  - **YouTube Music** — Connect with browser extensions (Safari · Chrome · Edge) (브라우저 확장과 연결 (Safari · Chrome · Edge)) (off by default) · **Open extension folder (확장 폴더 열기)** ([§8.1](#81-using-youtube-music-chrome-extension)).
  - **Lyrics internet search (가사 인터넷 검색)** — lrclib.net on/off in **Lyrics source (가사 출처)** in the sidebar's **Lyrics** tab (the **가사 탭에서 바꾸기 ›** link on the network-destination row here also goes there).
  - **AI lyrics translation (AI 가사 번역)** — found in the collapsed **AI provider settings** under **Translation steps (번역 단계)** in the sidebar's **Lyrics** tab. Off by default. **Provider (제공자)** (one of Anthropic Claude · OpenAI · Google Gemini) · **Model (모델)** · **API key (API 키)** (your own key; **키 저장** save · **키 삭제** delete; kept only in this Mac's login keychain) · **Turn on AI lyrics translation (AI 가사 번역 켜기)** · **Use a daily request limit (하루 요청 상한 사용)** · **Request size (요청 크기)** · **Test connection… (연결 시험…)** · **Delete all AI translations… (AI 번역 전부 지우기…)**. Pressing **켜기** (turn on) shows a confirmation that says what goes where: the lyric lines and the title · artist go directly to the provider you chose. Charges go to your own API account, and the connection test counts as one request. With AI translation enabled and translation lines visible, a request is made after the track settles; connection tests and retries also make requests. Charges from the AI provider are settled between you, the owner of the key, and the provider, and request counts and charges include per-track requests made while translation is enabled. The developer does not bear the charges for requests you pressed. This does not apply when an error in the app sends requests you did not press. When a request cap (daily or monthly) is reached the app says so on screen and continues with on-device translation, and it says so once at 80 % of a cap. A failed request is never retried automatically, stored translations are reused, and asking again for the same song within 10 minutes sends nothing. After 3 provider errors in a row it stops for the day. We recommend setting a monthly spending limit in your provider's console. Translations are for your own listening on this Mac; if you publish lyrics or translations elsewhere, that is your responsibility. Lyrics remain the property of their rights holders.
    The provider list also has **Translate on this Mac (Apple Intelligence) (Mac 안에서 번역 (Apple Intelligence))**, which translates with the Apple model on this Mac and needs no key. The lyrics never leave the Mac and it costs nothing; it needs macOS 26 or later, an Apple silicon Mac and Apple Intelligence turned on. When it cannot be used it is dimmed with the reason, and even with no provider chosen it is used first, automatically, when it is available.
  - **Network destinations (네트워크 목적지)** — each internet destination on and off, with what goes out · when · what is lost when off.
  - **Apple Music** — **Track hand-off through a Fidenne playlist (곡 넘김을 Fidenne 플레이리스트로)** (on by default, [§2.2](#22-bottom-playback-bar)).
  - **Beta diagnostics log (베타 진단 기록)** (whether to record diagnostics for problem reports automatically) · **Licences · third-party notices (라이선스 · 제3자 고지)** (read in the app with **View… (보기…)**).

### 8.1 Using YouTube Music (Chrome extension)

Listen to YouTube Music in Safari, Chrome or Edge. The sound is received by Fidenne Inlet and goes to Fidenne; the extension adds **track info and control** — the track shows in the bottom bar, and the bar's play · pause · next · previous control that tab. This is an **experimental feature** and may stop working when YouTube Music changes its pages. If another service is playing and a YouTube Music tab starts by itself (autoplay · resume), Fidenne stops that tab and leaves the song you were hearing (`스스로 재생을 시작한 YouTube Music 탭을 멈췄습니다 — 듣던 곡은 그대로입니다`, "stopped a YouTube Music tab that started playing by itself — your song is unchanged"). When you press play in that page yourself, or play a YouTube Music song from Fidenne, YouTube Music takes over the sound.

**One time only — installing the extension (developer mode)**

1. Turn on **YouTube Music (experimental)** in Settings › **General**.
2. Turn on **Connect with browser extensions (Safari · Chrome · Edge)** in Settings › **Privacy** › **YouTube Music**.
3. Press **Install guide… (설치 안내…)** in the same place. In the small guide window's header choose **Chrome** or **Edge**.
4. **① Copy address (주소 복사)** → paste it into the browser's address bar and press Return (`chrome://extensions` · `edge://extensions`).
5. Turn on **② Developer mode**.
6. **③** Press the new **Load unpacked** button. Press **Copy path (경로 복사)** in the guide window → in the folder picker **⌘⇧G** → **⌘V** → Return → **Open**.
7. **④** Reload the YouTube Music tab that was already open (⌘R).
8. **Tab-sleep exception** — if the browser puts unused tabs to sleep, YouTube Music cannot answer. In Chrome add `music.youtube.com` to Settings › Performance › Memory Saver › **Always keep these sites active**; in Edge to Settings › System and performance › Resource saving › **Never put these sites to sleep**. Safari has no per-site sleep exception; if the bar stops, reload that tab once.

**Did it work** — the guide window's last line reads **브라우저 1개 연결됨** (1 browser connected), and a track you play on music.youtube.com shows in the bottom bar.

**Using it**

- **Playing from the Streaming page** — choose **YouTube Music** as the service to see imported playlists · a search field. Pressing a track plays from it in a YouTube Music tab. If Chrome is closed, Fidenne opens it in the background.
- **If the browser blocks the first playback** — `브라우저가 첫 재생을 막았습니다 · 탭에서 ▶ 한 번` (the browser blocked the first playback · press ▶ once in the tab) appears. Press **브라우저에서 ▶ 한 번** (▶ once in the browser), press ▶ once in that tab, and from then on the bar's buttons work. Browsers do not let a page make sound by itself before a person has pressed something. In Edge, adding music.youtube.com to **Allow** at `edge://settings/content/mediaAutoplay` may make this one press unnecessary (not yet checked).
- **Several browsers** — when the extension is connected in more than one browser and you start playing YouTube Music in a browser other than the one chosen, Fidenne moves to that browser and shows one line, `재생 중인 브라우저: <name>` (browser playing: <name>). It does not move within a few seconds after a play command Fidenne itself sent, does not go back to a tab it just paused, and also moves when the chosen browser's connection drops while another browser is playing.
- **Saving playlists** — opening a playlist screen in YouTube Music saves the visible tracks to Fidenne's **My playlists** like `12곡 · 브라우저에서 · …` (12 tracks · from the browser · …). For a long list, scroll to the end to bring the rest. **Delete list (목록 지우기)** deletes only in Fidenne.
- **Adding with a right-click** — **Fidenne에 추가 ›** (Add to Fidenne) at the bottom of a track's menu (⋮) on music.youtube.com, or **이 곡 Fidenne에 추가 ›** (Add this song to Fidenne) in the browser's right-click menu, adds one track to **Fidenne 좋아요 (♥)** (Fidenne Liked), a Fidenne playlist or **새 재생목록…** (a new playlist, named “재생목록 N” — rename it in the app), and **이 목록 Fidenne에 추가** (Add this list to Fidenne) on a playlist adds the whole list.
- **Library** — opening a YouTube Music library screen (liked songs · playlists · albums · artists) yourself brings that list in. **Up next** shows the list Fidenne played, otherwise the tab's "Up next" list.
- **Volume · quality** — if the source line in Playback Chain shows the page volume below 100 %, it is orange — raise YouTube Music's volume bar to the top. For quality with Premium, set the profile picture › **Settings** › **Playback & restrictions** › **Audio quality** to **High**. During ads, Fidenne shows no track info and says only "광고 중" (ad playing).
- **After updating the app** — press reload (↻) once on the **Fidenne for YouTube Music** card in `chrome://extensions`. If a line `브라우저의 확장이 옛 판…` (the browser's extension is an old version…) remains, press **Open extension folder** and ↻ again.
- What passes is the track name · artist · album · length · position · queue · album art and the like, only inside this Mac. Developer-mode install is the way for Chrome and Edge, and Safari's extension is inside the app ([Using Safari](#using-safari)).
- **Saving** — **YouTube Music에 저장** (save to YouTube Music) in an album's header presses the save control on the open album page once ([§3](#3-streaming-page)). With an old extension only **YouTube Music에서 열기** (open in YouTube Music) shows instead of saving; do **After updating the app** above.

#### Using Safari

The Safari extension is bundled with Fidenne. Turn on **YouTube Music (experimental)** in Settings › General and allow the extension in Safari. The **Connect with browser extensions (Safari · Chrome · Edge)** switch controls Chrome and Edge; Safari connects separately.

1. First check that Fidenne is in the Applications folder. Opened from inside the downloaded .dmg or from the Downloads folder, Safari does not show the extension, and Fidenne's Safari card and Settings › Privacy › YouTube Music say `Safari 확장은 Fidenne을 응용 프로그램 폴더로 옮긴 뒤 다시 열어야 Safari에 보입니다.` (move Fidenne to the Applications folder and open it again for the extension to appear in Safari). Quit Fidenne, move the app to **Applications (응용 프로그램)** and open it from there.
2. Press **Open Safari Settings (Safari 설정 열기)** in Settings › Privacy › YouTube Music (the Safari card in the YouTube Music connect window has it too). If Safari's extension settings open, turn on Fidenne's YouTube Music extension. If only Safari opens and no extension settings show, turn it on in Safari › Settings › **Extensions (확장 프로그램)**.
3. Open music.youtube.com, press the Fidenne icon in the row of extension icons next to Safari's address bar, and allow the extension on this website (choosing **Always Allow** makes it a one-time step). The same permission is listed in Safari › Settings › **Websites**.
4. Reload that tab (⌘R).

**How to tell it worked** — when you play a track on music.youtube.com, the bottom bar shows it. Safari 18.4 or later is required. The Fidenne app can be in the Applications folder or in the Applications folder inside your home folder (not an app opened from inside the .dmg or from the Downloads folder). Safari can put an unused extension to sleep; if the bar stops, reload that tab once.

### 8.2 YouTube Music app window — not available now

Logging in to YouTube Music inside a Fidenne window is not available now. Use YouTube Music through the extension in [§8.1](#81-using-youtube-music-chrome-extension). If you once logged in through that window, quit Fidenne and delete the leftover web storage in Terminal with `rm -rf ~/Library/WebKit/*/WebsiteDataStore/5c0f7e2a-3b1d-4e8f-9a6c-2d7b8e1f4a90`, then sign out under "Your devices" in your Google account.

## 10. Sending a Support File

When something goes wrong, make a diagnostics bundle of what happened and send it.

1. Press **Help › Create diagnostics for a problem report…** (the same button is in Settings › General › Help).
2. If you agreed to the optional diagnostic record at first launch, it is already recording: make the bundle right after the problem, before quitting the app. If it is off, press **Start diagnostic recording (진단 기록 시작)** and make the bundle the next time the problem happens.
3. Check what goes in with **Create bundle and show contents (번들 만들고 내용 보기)**. The bundle is saved as a .zip file in your Downloads folder.
4. **Send by mail (메일로 보내기)** opens the Mail app with the address, subject and form filled in. If you use another mail service (Gmail and so on), **Copy mail form (메일 양식 복사)** beside it copies the same text to paste. Attach the .zip file from your Downloads folder yourself. If you paste the contents instead, they get cut off by length limits and the records from when the problem happened may be lost. If you cannot find the file, open "Downloads" in Finder. The app version and macOS version are already in the form and the bundle.

**Did it work** — a new message opens in Mail, and **Show .zip file (.zip 파일 보기)** selects the .zip file in Finder.

- **Mark That Something Was Off (방금 이상했음 표시)** — press ⌥⌃⌘K (also in the Help menu) when something sounds odd, and only that time is marked in the diagnostic record on this Mac, so the spot is easy to find in the bundle. It marks even if you did not agree to the diagnostic record, and nothing leaves the Mac. When you create a bundle, the export window separates **the times you marked yourself (직접 표시하신 시각)** from **things that happened that you did not check yourself (직접 확인하지 않으셨지만 이런 일도 있었습니다)** — such as sound breaks and stops found automatically — and you can choose per item whether it goes into the bundle.
- The bundle holds numbers and states, and the tracks heard in that time (time, service, rate and random per-track labels, up to the last 200; titles, artists and albums are masked). File paths · device names · accounts are not included.
- **Please send the diagnostics bundle by mail — do not post it in a GitHub issue.** You decide whether and where to send it; the app sends nothing. Reports and bundles you send may be read with AI tools (Anthropic's Claude and others) ([Privacy](../../../PRIVACY.en.md)). **Export support diagnostics…** in the Diagnostics menu makes the same bundle.
- What to write along with it is in [Troubleshooting Guide §9](TROUBLESHOOTING.md#9-if-that-still-does-not-work--what-to-collect-and-send).

## Beta notice and where to report

Fidenne is in **public beta**. Download it from `https://github.com/fidenne/fidenne/releases`. It needs an Apple silicon Mac and macOS 15 or later.

- Reporting by mail to **fidenne.support@gmail.com** is the default. In the repository's issues (the **Bug report** form) the symptom alone is enough. Send diagnostics bundles and security problems by mail rather than in an issue.
- Good to include: DAC and output mode · what you were doing when, and what you heard. The app version and macOS version are already in the mail form and the bundle.

Step by step: [Task guide §30](HOW-TO.md#30-get-the-beta-and-report-a-problem).
