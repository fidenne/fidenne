<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/MANUAL.md (the short listener's edition of 2026-10-13) -->

# Fidenne User Manual

## One-page summary

**What Fidenne is** — a macOS app that takes the sound of Apple Music, Spotify and YouTube Music, or the music files on this Mac, shapes it with EQ, Ostrum, crossfeed and a filter, and sends it to a **wired USB external DAC** (required). It needs an Apple silicon Mac and **macOS 26 or later**.

The app's screens are in Korean only for now, so on-screen names are given in English with the Korean original in parentheses.

**The five pages** (sidebar, ⌘1–⌘5)

- **Music (음악)** — pick a service, search and play, and resume from the home screen. ([§3](#3-music-page))
- **Library (보관함)** — reads the music folders on this Mac and shows them as songs · albums · playlists. ([§4](#4-library-page))
- **Listening History (청취 기록)** — view what you listened to by period and source, and export it. ([§5](#5-listening-history-page))
- **DSP** — Response graph, Equalizer (with Auto EQ), Ostrum, Crossfeed. ([§6](#6-dsp-page))
- **I/O · Diagnostics (입출력 · 진단)** — output mode, input and output devices (DAC), filter · DSD conversion, and the path the sound takes now. ([§7](#7-io--diagnostics-page))

**The three output modes** (`I/O · Diagnostics › Output mode (출력 방식)`, [§7.1](#71-independent-output-control--output-mode))

- **PCM Direct** — Fidenne does not process the sound. It goes playback app → macOS → DAC as is. The rate is not matched track by track but set once at start; if the rates differ, macOS converts.
- **DSD (DoP)** — Fidenne processes the sound and sends it to the DAC as DSD.
- **PCM 352.8 kHz** — Fidenne processes the sound and sends 352.8 kHz PCM (24 · 16-bit).
- With EQ · Ostrum · Crossfeed off, DSD and PCM 352.8 kHz apply no tone-changing processing, but the conversions that format needs (upsampling filter · DSD modulator · dither · headroom) still run.

**Mind the volume** — the first time you play, start with the DAC · amplifier volume low and raise it slowly while listening ([§1](#1-first-launch--the-five-step-first-run-setup)).

**Where to get help** — step-by-step tasks are in the [task-by-task instructions](HOW-TO.md), the first install is in the [install and use guide](../GUIDE.md) (Korean only), when something fails see the [Troubleshooting Guide](TROUBLESHOOTING.md), questions you may have are answered in [Questions and answers](EXPLANATIONS.md), and what the app cannot do yet is in [Known limitations](KNOWN_LIMITATIONS.md). To report a problem, see [§10](#10-sending-a-support-file) and [Beta notice and where to report](#beta-notice-and-where-to-report). **[Experimental]** (〔실험〕) marks an option the app itself labels "experimental".

## 0. At a glance

The path the sound takes: the sound of a playback app (received through Fidenne Inlet or the system tap) or the music files on this Mac → Fidenne → DSD (DoP) or PCM 352.8 kHz → DAC. **PCM Direct** is playback app → macOS → DAC and does not pass through Fidenne.

### What Fidenne does and does not do

It is built to follow each music service's terms and policies, and is changed when they change. The same text is the fourth step of the first launch, and you can read it again from the app menu › **Fidenne이 하는 것 · 하지 않는 것** (What Fidenne does and does not do).

**What it does**

- It takes the playback app's sound through the audio features macOS opens to apps (CoreAudio · audio capture), shapes it in real time and sends it to the DAC you chose.
- It reads the current track through the AppleScript the Music · Spotify apps offer themselves, and passes on play · pause · track skip.
- It reads the Apple Music library and catalogue through Apple's MusicKit (Apple Music API), only when you allow it.
- For YouTube Music, a Chrome · Edge extension you install yourself reports the open tab's track inside this Mac.
- Spotify search · playlists · playback control (Spotify Web API) turn on only when you enter the key of your own Spotify developer app.
- Listening history counts the current track the playback app shows through AppleScript (title · artist · album · length) and the time listened — local files by their file tags. It stays on this Mac and is never sent out.

**What it does not do**

- It does not save the sound or make files of it. There is no recording feature.
- It does not replace or bypass a music service subscription. Tracks play through each service's app and your account.
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
- **Kept on this Mac** — album covers (Spotify covers too) in the Caches folder and lyrics in the app's data folder, temporarily, for quick display. Both are removed 30 days after last use.

The full list is in [Privacy](../../../PRIVACY.en.md).

**Window layout** — the sidebar reads Music · Library · Listening History · DSP · I/O · Diagnostics, and ⌘1… follow that order. The gear-shaped **Settings… (설정…)** row at the bottom opens the Settings window, and the **GitHub** row opens the public repository page. The sidebar header shows only the name Fidenne; the version and build number are in the app menu › About Fidenne and in Settings › General. The window reopens at its last size and position, on the page you last viewed.

## 1. First launch — the five-step first-run setup

On first launch the "Fidenne 처음 설정" (Fidenne first-run setup) window appears. Move between steps with **Back (뒤로) / Next (다음)**.

1. **The DAC the sound goes to (소리가 나갈 DAC)** — pick the output device. "Choose later (나중에 고르기)" also works. If the device does not show, plug in the DAC and refresh.
   Use a USB DAC with its **USB mode on UAC 2.0** and **its own EQ off**. UAC 1.0 stops at 96 kHz, too low to carry DSD; an EQ inside the DAC computes the PCM again, so it cannot pass DSD (DoP) untouched and lowers the rates the DAC takes (the FiiO K15 stops at 192 kHz with its EQ on). Then DSD and PCM 352.8 kHz output do not start. Fidenne's own EQ works together with DSD.
2. **How to bring in the sound (소리를 가져오는 방법)**
   - **Fidenne Inlet** (recommended, chosen from the start) — receives the playback app's source rate as is. If it is not installed, press **Install… (설치…)**. macOS asks once for the administrator password and restarts the audio service, so all sound stops for a moment. You can also install it later on the I/O page.
   - **System tap (시스템 탭)** — works right away without installing. Receives at 48 kHz.
   - If you already use another loopback app, pick it later under **+ Other input device (+ 다른 입력 장치)** on the I/O page.
3. **What macOS will ask (macOS가 물어볼 것들)** — permissions are not asked now; macOS asks when you first use that feature (system audio · microphone · automation · media library). The screen says when each is asked and what does not work if you decline.
4. **What Fidenne does and does not do (Fidenne이 하는 것 · 하지 않는 것)** — read what Fidenne uses, what it does and what it does not do (the same text as in [§0](#what-fidenne-does-and-does-not-do)).
5. **Licence and internet connection (라이선스와 인터넷 연결)** — below the full terms are four boxes: **Agree to all (전체 동의)** · **[Required] I agree to the terms of use ([필수] 이용 약관에 동의합니다)** · **[Optional] Use internet features ([선택] 인터넷 연결 기능 사용)** · **[Optional] Diagnostics log for problem reports, kept on this Mac only ([선택] 문제 제보용 진단 기록(이 Mac에만 저장))**. **Start (시작)** works only after the required box. Without the optional boxes playback still works; only features that use the internet are off. **Quit without agreeing (동의하지 않고 종료)** quits the app. You can change the choices later in Settings › Privacy.

**Did it work** — the same window shows the sidebar and a page, and the setup does not appear again on later launches.

**The first time you play — the volume notice.** Each time the app starts, the first press of play shows one sheet "음량을 낮추고 시작하세요" (Lower the volume before you start) **before** any sound. Turn the DAC · amplifier volume to 0 or very low, press **낮췄어요, 시작** (I lowered it, start) (Return), then raise it slowly while listening. **Cancel (취소)** (Esc) starts nothing. It also appears once when you start with a DAC used for the first time ("○○을 처음 씁니다"). The only place to turn this notice off is Settings › **Sound safety (소리 안전)**, and even then it asks once for a new DAC.

**Output watch.** If a signal appears that music cannot produce (sound stuck at one extreme · large DC · a large inaudible ultrasonic signal), Fidenne mutes the rest of that playback and shows "출력을 음소거했습니다 — …" (Output muted — …) at the window's top. Stop and play again to get sound back. Ordinary sound is not changed.

**Internet.** Features that use the internet are turned on and off one by one in Settings › Privacy › **Network destinations (네트워크 목적지)**. With all of them off, receiving sound · DSP · DSD conversion · DAC output · file playback still work, and sound never leaves the Mac.

## 2. Always visible — header · bottom playback bar · menus

### 2.1 Page header

The **Playback Chain** button next to the page name shows the order the sound passes — **source → capture → conversion → band → DSP → filter → output → device** — one line each, with the current values.

- The dot and word in its header give the overall state: **Running · processed (실행 중 · 처리됨)** · **Running · no processing (실행 중 · 처리 없음)** (PCM Direct) · **Stopped (멈춤)** · **Preparing (준비 중)** · **Error (오류)**.
- The **source** line is the app making the sound now, the **capture** line is how and at what rate it is received (red if sound was dropped). The **conversion** line says whether the original and received rates match; if not, in red `44.1 kHz → 48 kHz · 재생 앱이나 macOS 가 바꿈` (changed by the playback app or macOS). Spotify does not report its original rate, so it reads `없음으로 추정` (assumed none).
- The **band** line measures where the incoming sound is cut off (for example `16.0 kHz 위로 소리가 거의 없음`, almost no sound above 16.0 kHz). It does not say why — it may be lossy compression or a trait of the original master.
- Pressing a chip on the **DSP** line (**EQ · Ostrum · Crossfeed**) turns it on and off right there. A line (or chip) ending in `›` takes you to that setting.
- If the output device is missing or disconnected, that line turns red and **Find again (다시 찾기)** · **Reconnect (다시 연결)** appear.

When something goes wrong, a red notice band appears at the window's top (for example `DAC 연결이 끊겨 재생을 멈췄습니다. 다시 연결한 뒤 재생을 누르세요.` — the DAC was disconnected, so playback stopped; reconnect it and press play). It closes by itself when the DAC comes back, or with ×.

### 2.2 Bottom playback bar

The bar floats on every page. In a wide window it is one row: album cover · track (title / artist) · playback buttons (shuffle · previous · play/pause · next · repeat) · heart | service icon · **output mode** · ⋯ · **Up next (다음 재생)** · **engine switch**. In a narrower window it becomes two rows — the cover spans both rows; the top row has the track · ⋯ · Up next · engine switch, and the bottom row the playback buttons · heart, then the service icon · output mode.

- **Position** — the line along the bottom of the bar, from the cover's lower right corner to just before the service icon. Press or drag it to move. When the pointer rests on it, the row right above it blurs and the elapsed and remaining times appear over its two ends.
- **Heart** — adds to Fidenne's own **Liked songs** in the library, separate from the service app's likes.
- **Service icon** — the app making the sound now. Only the icon shows, without a name; resting the pointer on it shows the name. Pressing it opens the current track in that service (for YouTube Music, its browser tab).
- **Output mode** — the label shows only the current output (for example `DSD256` · `PCM 24-bit`). Pressing it opens the menu: PCM Direct · sound presets (recommended list) · saved presets · "Sound settings… (사운드 설정…)". Details such as the filter and order are shown inside this menu. Choosing a saved preset switches to its output mode.
- **⋯** — the track menu ([§2.7](#27-track-menu---and-right-click)) and "Output settings… (출력 설정…)" (opens the filter card on the I/O page).
- **Up next (다음 재생)** — opens and closes the Up next · Lyrics column.
- **Engine switch** — turns Fidenne's processing (the engine) on and off. Its colour is the state (green running · orange preparing · red error). When the engine is off with an error, a red ! appears beside it; pressing it opens the I/O · Diagnostics page.
  - **The engine switch does not start a track, and the play button does not turn the engine off.** Pause stops only the playback app, and **Play** with the engine off turns it on and plays.
  - What plays when the engine starts is set by **After the engine starts (엔진 시작 후)** on the I/O page ([§7.3](#73-streaming-app-autoplay--input-and-output-devices)).
- Shuffle · repeat work only on lists played from Fidenne. Another app's queue is handled in that app.
- Click a song list's **#** · **Title (제목)** · **Album (앨범)** · **Time (시간)** head to sort by that column ascending; click again for descending, and once more for the list's own order (the sorted head shows ↑ ↓). Anywhere in the head's box works. **#** returns to the list's own order. It is the same state as the list's **Sort (정렬)** menu, playback follows the order on screen, and it is forgotten when the app quits.
- When a browser or another app starts making sound, the bar says **`시스템 소리 — 출처를 모름`** (system sound — unknown source), and meanwhile it does not count history or look up lyrics.
- When Spotify plays on another device (a phone etc.), the bar shows only **`Spotify — 다른 기기에서 재생 중`** (playing on another device). Control it on that device. If content scrolling behind the bar hides its text, change the material in Settings › General › **Playback capsule (재생 캡슐)**.

**Large playback view** — press the album cover in the bar. It has three columns: cover and controls · **Up next (다음 재생)** and **Lyrics (가사)** · **Playback Chain** (fold it with the `›` grip or **⌥⌘P**). **⌘F** searches over this view, and the service name (`Apple Music ↗` etc.) opens the current track in that service. Close with ×, by pressing the cover again, or **Esc**.

**Up next and Apple Music** — Apple Music does not tell other apps its upcoming tracks.

- When you play an Apple Music list from Fidenne, it puts the next tracks in a playlist **‘Fidenne 재생 대기열’** (Fidenne playback queue) in the Music library and plays from there, so no other track slips in between. It asks once before first use (**Continue (계속)** · **Turn off and continue (끄고 계속)**), and with iCloud library on, this playlist shows in Music on your other devices too. Turn it off in Settings › Privacy › Apple Music.
- For a track you started in the Music app, Fidenne reads which playlist · album it came from and shows the next tracks. If it cannot tell, **Continue this album (이 앨범 이어 듣기)** · **Back to the Fidenne list (Fidenne 목록으로 돌아가기)** · **Leave it to Apple Music autoplay (Apple Music 자동 재생에 맡기기)** appear.
- When Music picks another track by itself, **`Apple Music 자동 재생이 고른 곡`** (a track picked by Apple Music autoplay) appears. Turn off Music's autoplay (∞) to keep to the Fidenne list.


**If Fidenne controls Apple Music playback, turn these off in the Music app**

- **Autoplay (∞)** — the ∞ button above Music's Up Next. When on, Music inserts other tracks and the order changes.
- **Shuffle · Repeat** — turn them off in Music; use the shuffle · repeat on Fidenne's bar if you need them.
- **Song transitions (AutoMix · Crossfade)** — Music › Settings › Playback. Overlapping tracks blur when a track changes, so track changes and rate matching can go wrong.
- Things that change the sound first (**Sound Check** · **Equalizer** · **Sound Enhancer**) are best turned off too; they change the sound before Fidenne shapes it.

**When Fidenne plays a YouTube Music list** — turning off YouTube Music's **Autoplay** switch at the top of the Up next panel is recommended. With it on, Fidenne still stops a song Autoplay opens and plays the list's next song, but the song change is cleanest with it off.
### 2.3 Lyrics

When a track plays, the lyrics panel shows its lyrics. Internet lyrics (lrclib.net) need your consent once — "동의하고 찾기" (Agree and search) / "보내지 않음" (Do not send). Only the title · artist · album · length are sent.

| Control | What it does |
|---|---|
| **Link lyrics file (가사 파일 연결)** | Links an LRC · TXT file to this track (can be unlinked). |
| **Lyrics timing (가사 타이밍)** (clock button) | Opens from the clock button. + if lyrics are early, − if late. Applies to this track only and is remembered. |
| **Text linking (글자 연결)** | Fits an untimed lyrics file's text to the timing of the current lyrics. |
| **Korean translation (한국어 번역)** | Adds a Korean line under each line. Without a Korean version it uses macOS translation. |
| **Lyrics version (가사 판)** | Appears when two or more versions are known; picks one (original · romanized · English · Korean etc.). Find others with **Other version (다른 판)** in the source line. |
| Refresh (↻) | Searches once more. |

- Text size is in Settings › Display › **Lyrics text size (가사 글자 크기)** (small · normal · large).
- Even when an app spells a track differently (a Korean artist name · "- Remastered" etc.), it finds the lyrics if the title · length and the artist or album match. Another person's song with only the same title and length is not shown.

### 2.4 Menu bar icon · menus

- **Menu bar icon** (waveform) — status · start · stop · play/pause · open window · output device · **EQ presets ▸** (the last five; choosing one is heard at once) · quit. Start · stop are the same as the engine switch.
- **Hiding the icon** — turn Fidenne off in **System Settings › Menu Bar › Allow in the Menu Bar**. The window · Dock · shortcuts stay.
- **App menu** — "About Fidenne" (with the trademark notice), **Check for updates… (업데이트 확인…)**. It reads the public repository once and says "최신입니다" (up to date) or names the new version (or says there is no public release yet). For a new version it also shows a few lines of what changed. If you left the GitHub connection on at first run, it also checks once a day without being pressed and tells you about a new version (turn it off with the switch at the bottom of Network destinations). The app never downloads or installs by itself.
- **Help menu** — **Show controls (조작법 보기)** · **Create diagnostics for a problem report… (문제 제보용 진단 만들기…)** ([§10](#10-sending-a-support-file)). **Diagnostics menu** — start/stop diagnostics · **Export support diagnostics… (지원용 진단 내보내기…)** · **Delete saved diagnostics… (저장된 진단 삭제…)**.
- Deletions that cannot be undone (saved diagnostics · a playlist · shortcuts "all to defaults") ask once. The red button is not pressed by Return.
- **Shortcuts** — the list is in Settings › **Controls and shortcuts (조작과 단축키)**: change · clear · default per key. It warns about clashes with macOS shortcuts. They work only while the Fidenne window is in front (media keys excepted).
  **⌘S** saves the Equalizer or Ostrum on screen, and **⌘F** goes to the page's search field on Library · Listening History, otherwise to the Music search field.
  The keys that turn EQ · Ostrum on and off are heard at once but do not save.

### 2.5 Explanations · how to read graphs · glossary

- The line under a section title says what that feature does. Pressing **ⓘ** at its end opens a bubble: when to use it · what to put in · what changes · the cost. **Esc** or a click outside closes it.
- **Glossary (n) (용어 풀이)** in an explanation shows that part's terms, and **Show the whole glossary (용어집 전체 보기)** shows all of them. Under each graph the axes and line names are always visible; **ⓘ** at the end of that line explains each line, how to read it and what the graph cannot tell.
- Numbers in the app come from measurements, and the app never judges that a setting makes the sound better.

### 2.6 Handling knobs · sliders · EQ points

The first time you open Equalizer and Ostrum, a tip **EQ 다루기** (Handling the EQ) · **노브 다루기** (Handling knobs) appears next to the control once. To see it again: **Help › Show controls**, or Settings › Controls and shortcuts › **Show tips again (팁 다시 보기)**.

| Control | How |
|---|---|
| Knob (Ostrum) | Turn it in a circle or drag straight up and down (up = more). **Shift** · **⌥** fine-tune. **Double-click** or ⌥-click resets it. Press the number to type a value |
| EQ slider | Press or drag up and down. **Double-click** · ⌥-click is 0 dB |
| EQ number field | Press, type, **Return**. The arrows step one notch. ⌥-click is the default |
| Graph point (EQ) | Dragging changes frequency and gain together. **Shift** · **⌥** move ten times slower. Pressing a point selects it; drag the small ring beside it sideways for Q. Double-click empty space to add a band |
| Position · other sliders | Press or drag |

- **Two-finger scrolling** always moves the page. A value changes only when you keep **⌘ held** with the pointer on the control (scroll up = up); add ⌥ · Shift for slower. Choose the behavior in Settings › Controls and shortcuts › **Change values with two-finger scrolling (두 손가락 스크롤로 값 바꾸기)** (with ⌘ held · when started over a control · off).
- **Trackpad haptics** — **Off · ends only · normal (끔 · 양끝 알림 · 일반)** in Settings › Controls and shortcuts. On a Force Touch trackpad a light tap per notch while dragging.
- **Music page back · forward** — the ‹ › buttons, ⌘[ ⌘], a sideways trackpad swipe and the **mouse side buttons** (back · forward) all make the same step. The side buttons work only while the Fidenne window is in front.
- **⌘Z / ⇧⌘Z** — step back and forward through changes made on the DSP page (one whole drag is one step). Undone values are heard at once.

### 2.7 Track menu — ⋯ and right-click

Wherever a track is a row (Music · Up next · Library · Listening History), **⋯** at the row's end or a **right-click** opens the same menu. Items that cannot be done for that row are not shown.

1. **Play (재생)** · **Play next (다음에 재생)** · **Add to end of queue (대기열 끝에 추가)**
2. **Add to playlist ▸ (재생목록에 추가)** · **Show lyrics (가사 보기)** · **Track info (곡 정보)** · **Open in Apple Music (Apple Music에서 열기)** · **Show in playback app (재생 앱에서 보기)** · **Show in Finder (Finder에서 보기)** · **Copy link (링크 복사)** (with two or more places to open, they are grouped under **Open in another app ▸ (다른 앱에서 열기)**)
3. **Remove from playlist… (재생목록에서 빼기…)** (asks once; files stay) · **Remove from queue (대기열에서 빼기)**

Spotify tracks have **Open in Spotify (Spotify에서 열기)** · **Copy link**. There is no menu for many tracks at once yet.

## 3. Music page

Where you search and open Apple Music · Spotify · YouTube Music in one place.

- **Choosing a service** — pick **Apple Music** · **Spotify** · **YouTube Music** from the service button before the search field. YouTube Music needs the extension in [§8.1](#81-using-youtube-music-chrome-extension).
- **Search** — results come on one screen in order: my Apple Music (library · playlists) → the Apple Music catalogue (tracks not in the library) → files on this Mac. The last line **Find ‘query’ in YouTube Music ↗** opens the same search in a YouTube Music tab.
  - **Spotify results are separate** — press the **Spotify** tab at the top of the results, and the **Apple Music · Local** tab to come back. Spotify asks that its content not be placed next to other services' results.
  - **Add to library (보관함에 추가)** — puts a catalogue track · album into the Apple Music library. A confirmation appears the first time (the library changes; with iCloud library it shows on other devices). It takes a while to appear, so "보관함에 나타나는 중" (appearing in the library) shows until the button becomes **Play**.
- **Pressing a track** — **Play next** / **Play now (지금 재생)**. **Play all (전체 재생)** · **Shuffle (셔플)** over a list go through it once without repeats. A long Apple Music list may show **재생 준비 중…** (preparing playback…) the first time; to shuffle, turn **Shuffle** on before playing.
- **Home screen** — **Continue listening (이어 듣기)**, **Listened today (오늘 들은 것)** (on later days **Recently listened (최근 들은 것)**), **My playlists (내 재생목록)**, **It's been a while (오랜만에)**. ▶ on a Continue card plays that card's service and track, from the saved position if there is one. **Open list (목록 열기)** opens the list the track was heard from.

**Connecting Spotify (optional)** — even without a key, when you pick a track in the Spotify app Fidenne shapes its sound and shows the current track. Search · playlists · playback control turn on only with **the key of your own Spotify developer app**, whose terms you agreed to.

1. Press **Open developer dashboard (개발자 대시보드 열기)** in the Spotify settings box and create an app.
2. Put the address shown in the box into that app's Redirect URI (the **Copy (복사)** button beside it).
3. Paste the dashboard's **Client ID** into the box. Do not enter the Client Secret.
4. Press **Check key (키 확인)**, and if it is right, **Connect Spotify (Spotify 연결)**. The Spotify login window opens in the browser.

After connecting you see "Refresh playback permission (재생 권한 갱신)" · "Disconnect (연결 해제)". **Follow Spotify queue · for Jam (Spotify 대기열 따르기 · Jam용)** keeps Fidenne from overwriting a Spotify shared queue.

**Did it work** — pressing a track shows its name and service icon in the bottom bar, and the position moves.

## 4. Library page

Where you listen to music files on this Mac. Formats read: WAV · AIFF · FLAC · ALAC · AAC · MP3 · Opus (when macOS can read it). `.ogg` · `.oga` do not play yet.

1. The first time, press **Add folder… (폴더 추가…)** and choose your music folder.
2. When indexing is done, find tracks in **Songs · Albums · Artists · Playlists (노래 · 앨범 · 아티스트 · 재생목록)**.
3. Press a row to play from that track.

**Did it work** — rows show cover · title · format (for example FLAC · 96 kHz · 24-bit) · length, and pressing one shows it in the bottom bar.

- **Music folders (음악 폴더)** menu — Add folder… · **Re-index (다시 색인)** · Remove folder from list ▸ (only from the list; files on disk stay).
- **Songs** — the search field (⌘F) filters the current list. A file that cannot play shows the reason (`손상된 파일`, damaged file, etc.) in the format column. **Albums · Artists** are grouped by file tags.
- **Playlists** — enter a name and create one. Inside: Play all · Shuffle · Delete… (deletes only the playlist; files stay). "파일을 찾을 수 없음" (file not found) means a folder was removed or the file moved.
- **Selecting several · reordering** (playlists · Up next) — select with ⌘-click · Shift-click, and drag a row onto another to move it. **Return** plays the first selected track.
- **Up next** — the **Up next (다음 재생)** button in the bottom bar shows the current and upcoming tracks. Tracks of the same rate play without a gap; where the rate changes there is a short break.
- Files always play through Fidenne. Even with PCM Direct as the output mode, files go out through Fidenne's PCM output.

**YouTube Music playlists** collect not on this page but in `Music › YouTube Music › My playlists`. There are two ways in — opening a list screen in the browser ([§8.1](#81-using-youtube-music-chrome-extension)) and a Google Takeout file ([§4.1](#41-importing-youtube-music-playlists)). Fidenne never walks the YouTube Music site by itself. What you can do on an imported track row:

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
6. In Fidenne, open **YouTube Music library (YouTube Music 보관함)** at the bottom of `Music › YouTube Music › My playlists`, press **Import YouTube Music playlists… (YouTube Music 재생목록 가져오기…)** and choose the whole unpacked `Takeout` folder.

**Did it work** — a line `재생목록 N개 · M곡 · …` (N playlists · M tracks · …) appears and the lists show in My playlists.

- Choosing the whole folder gives tracks their names. With only the playlist files they show as `이름 모르는 항목` (unnamed item).
- Importing the same list again replaces it. **Delete…** removes only the list imported into Fidenne.

## 5. Listening History page

Where you see what you listened to on this Mac. Nothing is uploaded automatically; you can only export it yourself.

- **Period** — 1 day · 1 week · 1 month · 6 months · 1 year. **Source** — all · Apple Music · Spotify · local. **Graphs** — play trend · where you listened · top artists · genre and tempo.
- **What counts as one play** — while Fidenne is open, 30 seconds of actual playback or half the track (whichever is shorter). Nothing is recorded while the app is closed.
- **Per-track history** — filter by track · artist · album (⌘F). The same song heard on Apple Music and Spotify is merged into one row with per-service counts, and the row says what the merge was based on. The "연결 후보" (link candidates) screen for joining songs that are only similar is hidden in this beta.
- **Local files** — only the tags (title · artist · album) are kept; file paths · folder names · file names are not.
- **Export** — JSON · CSV (the chosen source only). **Delete** — **Delete listening history (청취 기록 지우기)** in the fold **History settings and counting rules (기록 설정과 집계 기준)** → **Delete all (모두 지우기)**. This cannot be undone. Turning off **Keep listening history on this Mac (이 Mac에 청취 기록 저장)** stops recording.
- Genre · BPM use only what the playback app gives. Missing values are not guessed.

## 6. DSP page

Where you shape the sound. The header shows the current input rate (when stopped, based on the last playback). From the top: the **Response graph**, the tabs **Equalizer · Ostrum · Crossfeed** below it, and the chosen tab's details.

- **Changes are heard at once; save (⌘S) to keep them for the next launch.** The same for EQ and Ostrum. Edits stay when you visit another page and come back.
- Button and field names are in English, notices and warnings in Korean. DSP is heard only on outputs Fidenne processes (DSD · PCM 352.8 kHz); PCM Direct does not pass through it.

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

Header: **Equalizer** ⓘ · **EQ On** · **Presets ▾ (프리셋)** · **Back to saved (저장본으로 되돌리기)** · **Reset (초기화)** · **Save (저장)** (⌘S).

1. Change bands by dragging a graph point or with a slider · number field in the band columns. It is heard at once.
2. When you like it, press **Save** (⌘S).

**Did it work** — the line under the header reads `✓ 저장됨 · 다음 실행에도 이 EQ 로 시작합니다` (saved · the next launch starts with this EQ). Before saving it is the orange `● 저장 안 됨 — 저장(⌘S)해야 다음 실행에도 남습니다` (not saved).

- **Presets ▾** — keep a named EQ and choose it again.
  - The **recent** five and **All presets**. Choosing one is heard at once and the next launch starts with that EQ. The headphone · target the preset was fitted to and its strength come into the Auto EQ row with it, and **Bands** becomes that EQ's band count (100 % for a preset kept without a strength).
  - With a preset chosen, saving (⌘S) also overwrites **that preset** with the EQ and the headphone · target. Changing only the headphone · target also turns Save on.
  - **Save as… (다른 이름으로 저장…)** saves the current EQ and keeps it under a new name (the current preset is untouched; up to 100). **Manage presets… (프리셋 관리…)** renames · deletes, and **Back to an earlier save (이전 저장본으로 되돌리기)** holds the EQ that was there before each save (the last 20).
- **Back to saved** returns to the last saved EQ, **Reset** sets all bands and the Preamp to 0 dB (flat). Both are heard at once.
- Quitting with an unsaved EQ playing asks once — save and quit · quit without saving · cancel.
- **Band columns** — **Preamp** first, then per band an on box and number · gain slider · type (PK · LS · HS · LP · HP · BP · NO · AP · G) · channel (L+R · L · R) · Gain · Freq · Q fields. Above the columns: **Open EQ Preset…** · **Graphic 31** · **Add Band** · **Delete Band** · **Reset Band**. Up to 32 bands; **Open EQ Preset…** opens AutoEq · Equalizer APO files.
- **Clipping & Headroom** (under the band columns) — whether this playback clipped, the limiter, and the **Apply Headroom N dB** suggestion button.
- **EQ Backend** — **Parametric** (default, no delay) / **Minimum-phase FIR** / **Linear-phase FIR** (about 0.2 s delay, from the next playback start). With linear phase, **Linear Phase Length** chooses the length. Which sounds better has never been checked.
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

1. Choose your headphone in **Headphone ▾**. If it is not listed, **Search headphones… (헤드폰 검색…)**.
2. Choose the goal in **Target ▾** — the measurer's target curve (DF · DF t · Harman …) or another headphone.
3. Press **Auto fit** at the row's end ([§6.6](#66-bands--strength--auto-fit-the-auto-eq-row-of-equalizer--what-auto-fit-did-collapsible)).

**Did it work** — the folded row reads like `Auto EQ   my headphone → goal · 10 bands`.

- Choosing a headphone · goal does not change the EQ. It changes when you press Auto fit.
- **Search headphones…** — downloads squig.link's measurement list and searches it on this Mac (the query is not sent). Press **Get list (목록 받기)** the first time; a received list is not downloaded again for 30 days. Pressing a row opens a check box, and it changes only when you press **Apply (적용)** (Return). **☆** marks a favourite (my headphones · target headphones are kept apart).
- If my headphone and the goal were measured on different rigs, the status line says so and **Rig difference correction (측정기 차이 보정)** (on by default) adjusts it. Goals whose rig relation cannot be known are hidden from the list. A goal of another kind (a headphone with an earphone target, for example) gets a yellow line and is not blocked.
- **Advanced — files · treble · Generative AI** (fold):
  - **Open from file** — **Open measurement…** · **Open target…** open your own measurement · target file (two-column Hz · dB text).
  - **Treble (Auto fit)** — how far to correct the treble (all · none above the boundary · half above 6–8 kHz etc.). Applied when you press Auto fit.
  - **Refine with generative AI (생성형 AI로 다듬기)** — **Copy text for the AI (AI에 줄 글 복사)** or export a file, refine it in the generative AI you use (ChatGPT · Claude etc.), paste the answer and press **Import the pasted answer (붙여 넣은 답 가져오기)**. The app sends nothing.

### 6.6 Bands · Strength · Auto fit (the Auto EQ row of Equalizer) · What auto fit did (collapsible)

- **Bands** — the number of bands. **8 · 10 · 12 · 16** buttons or the slider (1–32). 10 is the default. If a narrow wiggle remains at 4–8 kHz after fitting, raise it to 12–16 and fit again.
- **Strength** — correction strength (0–100 %, default 100 %). Lowering it scales every band's gain by the same ratio.
- **Auto fit** — the fitted bands go into the band columns and are **heard at once**. Save (⌘S) to keep them. If it cannot fit, the button is off and the reason shows in orange.
- **What auto fit did (자동 맞춤이 한 일)** (fold) — one sentence per band (for example "3 kHz 부근 4.0 dB 줄임 — 중고역 …", cut 4.0 dB near 3 kHz — upper mids …) and the error figures. It is not a judgment that the sound is good.
- With Ostrum on, Auto fit fits only the EQ, so the **After correction** line may look off the target.

### 6.7 The A/B button's panel — A/B · ABX · Auto Bypass · Loop · Level-matched Comparison (음량 맞춤)

A/B · ABX · Auto Bypass · Loop comparison is **hidden in this beta** — the DSP page shows no A/B button. It comes back once it is fixed ([Known limitations](KNOWN_LIMITATIONS.md)).

## 7. I/O · Diagnostics Page

### 7.1 Independent output control · Output mode

Choose one of three in **Output mode (출력 방식)** at the top of the page. A line under it says what the sound passes through.

- **PCM Direct** — Fidenne does not process the sound. It goes playback app → macOS → DAC as is. The sample rate is not matched track by track (because the sound does not pass through Fidenne, it cannot change the output rate to the track's (input) rate): when the DAC's rate and the track's differ, macOS converts. The DAC's rate is set once at start (44.1 kHz for Spotify; if the DAC was left at a rate that is not ordinary PCM, such as DSD or 352.8 kHz, the track's rate, or 44.1 kHz when unknown).
- **DSD (DoP)** · **PCM 352.8 kHz** — with EQ · Ostrum · Crossfeed off there is no tone-changing processing. The conversions the format needs (upsampling filter · DSD modulator · dither · headroom) still run, and the character of the sound may vary with the filter and modulator you choose. PCM 352.8 kHz then chooses **bit depth** (24 · 16-bit) and **dither** below it.
- Check the DAC volume before switching to PCM Direct — Fidenne's headroom does not apply, so it may sound louder.

The chosen output mode stays for the next launch. DSD · PCM 352.8 kHz are restored only if that format was confirmed on that DAC before; otherwise it **starts in PCM Direct** and says so in one line. Opening the app alone never starts sound.

- **Output DAC** — choose · refresh · reconnect. Devices that do not take 352.8 kHz (built-in speakers · AirPods · most dongles) get `· PCM Direct 만` (PCM Direct only) after the name; DSP and library playback do not work on them. A USB DAC plugged into another port is still recognised; when unsure it asks once: **Use as the same device (같은 장치로 쓰기)** / **Use as a different device (다른 장치로 쓰기)**.

### 7.2 DAC format check (formerly "Engine output format")

A table of which formats your DAC takes (DSD128 · DSD256 · PCM 24 · 16-bit). Each shows **Confirmed (확인됨)** (✓) · **Refused by the engine (엔진이 거절함)** (⚠ + reason) · **Not yet checked** · **Unknown (모름)**, remembered per DAC.

- **Check all (모두 확인)** — pressed while stopped, it tries each unchecked format in turn and restores the original. No sound plays, but the DAC may click or its display may change briefly.
- If the DAC does not take the chosen format, Fidenne does not drop to another rate; it does not start.
- **It asks once the first time it sends DoP** — `<DAC 이름>로 DSD(DoP)를 처음 보냅니다` (sending DSD (DoP) to <DAC> for the first time). Confirmed in the table does not mean the DAC decodes DoP; a DAC that cannot plays loud noise.
  Lower the volume or take off the headphones; if the DAC's manual lists DoP press **DoP를 받는 DAC · 시작** (DAC takes DoP · start), otherwise **PCM 24-bit로 재생** (play as PCM 24-bit). Check that the DAC's indicator shows DSD; if you chose wrongly, **Ask again (다시 묻기)** on the DoP line under the table.
- With a DAC whose volume control is linked to the macOS volume, Fidenne takes that volume over for DSD · integer PCM output: it plays at the same loudness by lowering the sound inside Fidenne, and gives the volume back afterwards. The output device line in Playback Chain shows `DAC 음량 −○ dB 를 Fidenne 이 넘겨받음` (Fidenne took over the DAC volume of −○ dB). If it cannot, you see `이 DAC 의 음량을 Fidenne 이 넘겨받지 못했습니다` (Fidenne could not take over this DAC's volume) — listen to that DAC with PCM Direct ([Troubleshooting](TROUBLESHOOTING.md#dac-volume-and-dsd-dop--integer-pcm)).
- **If the DAC reconnects within N seconds, resume (DAC가 N초 안에 다시 연결되면 이어서 재생)** — waits for the same DAC only. "Don't wait (기다리지 않기)" turns it off.
- It starts even if another app is using the DAC. If that app does not let go, `다른 앱(…)이 DAC에서 물러나지 않아…` (another app did not move away from the DAC…) shows once and it does not retry. Meanwhile the other app's sound may move to the Mac speakers.
- If `DAC 재생 통로가 macOS 안에서 멈췄습니다…` (the DAC playback path stopped inside macOS…) appears, unplug and replug the USB cable or restart Fidenne ([Troubleshooting Guide](TROUBLESHOOTING.md)).

### 7.3 Streaming-app autoplay · Input and output devices

**After the engine starts (엔진 시작 후)** — what to do when the engine turns on. **Auto-detect (자동 감지)** starts no track and follows the app that is playing (for browser sound, keep this and play in the browser). **Apple Music** · **Spotify** play that app's current item, **YouTube Music (browser)** sends ▶ to the open tab. **No autoplay (자동재생 안 함)** only turns the engine on. When Music and Spotify play at once, Fidenne follows the one started last and pauses the other.

**Input** — how the sound is received. The chosen input carries over to the next launch.

- **Fidenne Inlet** (recommended) — receives the playback app's source rate as is. **Install… / Update… / Remove… (설치… / 업데이트… / 제거…)** in the same box. Installing · removing asks for the administrator password and briefly silences all apps — do it when you are not listening. Alert sounds do not go to Fidenne Inlet. If the device's rate is changed during playback, it goes quiet for 1–3 s and continues at the new rate. If "옛 이름으로 설치되어 있습니다" (installed under the old name) shows, install again (your choice of input stays).
- **System tap (시스템 탭)** (listed as **Process Tap**) — receives all apps' sound on this Mac at 48 kHz without installing. While receiving, that sound plays only through Fidenne, and turning the engine off returns it at once. macOS asks for audio recording permission on first use — if declined it is silent (System Settings › Privacy & Security › Screen & System Audio Recording). To receive only one app's sound, send that app's output to Fidenne Inlet and choose Fidenne Inlet as the input.
- **+ Other input device (+ 다른 입력 장치)** — picks another loopback device you already use (only devices with both an output and a 2-channel input; remove with **✕**).

**Apple Music source rate** — the input rate follows each Apple Music track's source rate. Fidenne remembers on this Mac the rate of tracks you played, so next time they start at the right rate. For a track heard for the first time, the first sound is held briefly (usually under 1 s, at most 2 s) until the rate is known. Spotify does not report its source rate, so it is set to 44.1 kHz.

### 7.4 Filter · Modulator · Output gain (card) — sound settings for the DSD path

The sound settings for DSD · PCM 352.8 kHz output. The card shows the current **filter** · **output** · **gain** one per line, and **Details (자세히)** opens ①–③.

The **Recommended combinations N (추천 조합 N개)** fold in the **Where shall we start listening? (어디서부터 들어볼까요?)** card holds recommendations by purpose. Each card says what to listen for, and changes only what it lists. Choosing one during playback pauses briefly and continues.

1. **Filter** — processing type (standard SRC · long-tap extension · ultra-long-tap) · family · length. A filter with an [Experimental] badge states its caveat. Long and ultra-long filters delay the sound, so they show **delay ○○ ms** as a warning that video may drift — for video, standard SRC and the **Low latency (저지연)** buffer drift least. The fold **Choose by conditions · compare costs (조건으로 고르기 · 비용 비교)** filters by maximum delay · CPU. The 20 Hz–18 kHz response is practically the same for all filters; what differs is above 20 kHz and the time response.
2. **DSD conversion** — modulator **7th order · default** / 5th order · protected, output rate DSD128 / DSD256. DSD256 becomes the default once confirmed on that DAC.
   - **Buffer (버퍼)** — low latency · standard · **stable (default)**. Sound quality is the same; only how soon a change is heard and how well it resists dropouts differ. Change it while stopped; it applies from the next playback.
   - **Experimental · dither order N** [Experimental] — change it while stopped; applies from the next playback (not checked by listening).
3. **PCM headroom (PCM 헤드룸)** — **Auto (recommended) (자동 (권장))** is the default. It lowers the whole signal by what EQ · Ostrum raised, to prevent clipping. Changing it with the slider · buttons makes it **manual**, and **Back to auto (자동으로 되돌리기)** returns. It is auto again after relaunch. It is not the DAC volume — set the listening level on the DAC.

- **Save current sound preset (현재 사운드 프리셋 저장)** — saves ① filter · ② DSD conversion (with experimental dither) · ③ headroom as one preset. Saved presets can also be chosen from the output mode menu in the bottom bar.
- **Current selection guide (현재 선택 가이드)** — what the chosen filter changes, where to listen, what it costs, and its frequency response graph.
- If the 7th-order modulator needed stabilising, it shows the count and suggests "보호형 5차로 바꾸기" (switch to protected 5th order) · "DSD256 으로 바꾸기" (switch to DSD256).

### 7.5 Playback Chain · Actual behavior · Diagnostics

- **Playback Chain** card — the same as in the window header ([§2.1](#21-page-header)). If "출력은 안전하게 정지했습니다." (output stopped safely) appears, press **Reconnect DAC (DAC 다시 연결)**.
- **Actual behavior · diagnostics (실제 동작 · 진단)** (fold) — requested and actual rate, remaining headroom, estimated output delay, dropped-sound · underrun counts. The delay is a software estimate, not a measurement of the DAC's analogue output.

## 8. Settings Window

Open it with **⌘,** · **Settings… (설정…)** in the app menu · the **Settings…** row at the bottom of the sidebar. Changes apply at once and stay for the next launch.

- **General (일반)** — **YouTube Music (experimental) (YouTube Music (실험 기능))** (when off it does not appear in the service list or the playback capsule; off on a fresh install) · version and **Check for updates…** · **Interface scale (인터페이스 배율)** · **Theme (테마)** (system / light / dark; dark on a fresh install; light is not a finished theme yet) · **Liquid Glass** · **Playback capsule (재생 캡슐)** (material · transparency) · **Motion effects (동작 효과)** · **Restore display defaults (화면 설정 기본값 복원)** · **Help (도움말)** (diagnostics for problem reports, [§10](#10-sending-a-support-file)).
- **Controls and shortcuts (조작과 단축키)** — two-finger scrolling · trackpad haptics · **Show controls** · **Show tips again** · the shortcut list ([§2.4](#24-menu-bar-icon--menus)).
- **Sound safety (소리 안전)** — **Volume notice at every start (켤 때마다 음량 안내)** (on by default) · **Mute when a signal not found in music appears (음악에 없는 신호가 나오면 음소거)** (on by default). See [§1](#1-first-launch--the-five-step-first-run-setup).
- **Privacy (개인정보)**
  - **YouTube Music** — Connect with the Chrome · Edge extension (Chrome · Edge 확장과 연결) (off by default) · **Open extension folder (확장 폴더 열기)** ([§8.1](#81-using-youtube-music-chrome-extension)).
  - **Lyrics internet search (가사 인터넷 검색)** — lrclib.net lyrics on/off.
  - **Network destinations (네트워크 목적지)** — each internet destination on and off, with what goes out · when · what is lost when off.
  - **Apple Music** — **Track hand-off through a Fidenne playlist (곡 넘김을 Fidenne 재생목록으로)** (on by default, [§2.2](#22-bottom-playback-bar)).
  - **Beta diagnostics log (베타 진단 기록)** (whether to record diagnostics for problem reports automatically) · **Licences · third-party notices (라이선스 · 제3자 고지)** (read in the app with **View… (보기…)**).

### 8.1 Using YouTube Music (Chrome extension)

YouTube Music has no Mac app, so you listen in Chrome (or Edge). The sound is received by Fidenne Inlet and goes to Fidenne; the extension adds **track info and control** — the track shows in the bottom bar, and the bar's play · pause · next · previous control that tab. This is an **experimental feature** and may stop working when YouTube Music changes its pages.

**One time only — installing the extension (developer mode)**

1. Turn on **YouTube Music (experimental)** in Settings › **General**.
2. Turn on **Connect with the Chrome · Edge extension** in Settings › **Privacy** › **YouTube Music**.
3. Press **Install guide… (설치 안내…)** in the same place. In the small guide window's header choose **Chrome** or **Edge**.
4. **① Copy address (주소 복사)** → paste it into the browser's address bar and press Return (`chrome://extensions` · `edge://extensions`).
5. Turn on **② Developer mode**.
6. **③** Press the new **Load unpacked** button. Press **Copy path (경로 복사)** in the guide window → in the folder picker **⌘⇧G** → **⌘V** → Return → **Open**.
7. **④** Reload the YouTube Music tab that was already open (⌘R).
8. **Tab-sleep exception** — if the browser puts unused tabs to sleep, YouTube Music cannot answer. In Chrome add `music.youtube.com` to Settings › Performance › Memory Saver › **Always keep these sites active**; in Edge to Settings › System and performance › Resource saving › **Never put these sites to sleep**.

**Did it work** — the guide window's last line reads **브라우저 1개 연결됨** (1 browser connected), and a track you play on music.youtube.com shows in the bottom bar.

**Using it**

- **Playing from the Music page** — choose **YouTube Music** as the service to see imported playlists · a search field. Pressing a track plays from it in a YouTube Music tab. If Chrome is closed, Fidenne opens it in the background.
- **If the browser blocks the first playback** — `브라우저가 첫 재생을 막았습니다 · 탭에서 ▶ 한 번` (the browser blocked the first playback · press ▶ once in the tab) appears. Press **브라우저에서 ▶ 한 번** (▶ once in the browser), press ▶ once in that tab, and from then on the bar's buttons work. Browsers do not let a page make sound by itself before a person has pressed something. In Edge, adding music.youtube.com to **Allow** at `edge://settings/content/mediaAutoplay` may make this one press unnecessary (not yet checked).
- **Saving playlists** — opening a playlist screen in YouTube Music saves the visible tracks to Fidenne's **My playlists** like `12곡 · 브라우저에서 · …` (12 tracks · from the browser · …). For a long list, scroll to the end to bring the rest. **Delete list (목록 지우기)** deletes only in Fidenne.
- **Adding with a right-click** — **Fidenne에 추가 ›** (Add to Fidenne) at the bottom of a track's menu (⋮) on music.youtube.com, or **이 곡 Fidenne에 추가 ›** (Add this song to Fidenne) in the browser's right-click menu, adds one track to **Fidenne 좋아요 (♥)** (Fidenne Liked), a Fidenne playlist or **새 재생목록…** (a new playlist, named “재생목록 N” — rename it in the app), and **이 목록 Fidenne에 추가** (Add this list to Fidenne) on a playlist adds the whole list.
- **Library** — opening a YouTube Music library screen (liked songs · playlists · albums · artists) yourself brings that list in. **Up next** shows the list Fidenne played, otherwise the tab's "Up next" list.
- **Volume · quality** — if the source line in Playback Chain shows the page volume below 100 %, it is orange — raise YouTube Music's volume bar to the top. For quality with Premium, set the profile picture › **Settings** › **Playback & restrictions** › **Audio quality** to **High**. During ads, Fidenne shows no track info and says only "광고 중" (ad playing).
- **After updating the app** — press reload (↻) once on the **Fidenne for YouTube Music** card in `chrome://extensions`. If a line `브라우저의 확장이 옛 판…` (the browser's extension is an old version…) remains, press **Open extension folder** and ↻ again.
- What passes is the track name · artist · album · length · position · queue · album art and the like, only inside this Mac. It is not in the web store yet (developer-mode install only). Safari is not supported.

### 8.2 YouTube Music app window — not available now

Logging in to YouTube Music inside a Fidenne window is not available now. Use YouTube Music through the extension in [§8.1](#81-using-youtube-music-chrome-extension). If you once logged in through that window, quit Fidenne and delete the leftover web storage in Terminal with `rm -rf ~/Library/WebKit/*/WebsiteDataStore/5c0f7e2a-3b1d-4e8f-9a6c-2d7b8e1f4a90`, then sign out under "Your devices" in your Google account.

## 10. Sending a Support File

When something goes wrong, make a diagnostics bundle of what happened and send it.

1. Press **Help › Create diagnostics for a problem report…** (the same button is in Settings › General › Help).
2. If you agreed to the optional diagnostic record at first launch, it is already recording: make the bundle right after the problem, before quitting the app. If it is off, press **Start diagnostic recording (진단 기록 시작)** and make the bundle the next time the problem happens.
3. Check what goes in with **Create bundle and show contents (번들 만들고 내용 보기)**.
4. **Send by mail (메일로 보내기)** opens the Mail app with the address, subject and form filled in. If you use another mail service (Gmail and so on), **Copy mail form (메일 양식 복사)** beside it copies the same text to paste. Attach the bundle yourself. The app version and macOS version are already in the form and the bundle.

**Did it work** — a new message opens in Mail, and **Open bundle folder (번들 폴더 열기)** shows the bundle file.

- The bundle holds numbers and states, and the tracks heard in that time (title · artist · service, up to the last 200). File paths · device names · accounts are not included.
- **Please send the diagnostics bundle by mail — do not post it in a GitHub issue.** You decide whether and where to send it; the app sends nothing. Reports and bundles you send may be read with AI tools (Anthropic's Claude and others) ([Privacy](../../../PRIVACY.en.md)). **Export support diagnostics…** in the Diagnostics menu makes the same bundle.
- What to write along with it is in [Troubleshooting Guide §9](TROUBLESHOOTING.md#9-if-that-still-does-not-work--what-to-collect-and-send).

## Beta notice and where to report

Fidenne is in **public beta**. Download it from `https://github.com/fidenne/fidenne/releases`. It needs an Apple silicon Mac and macOS 26 or later.

- Reporting by mail to **fidenne.support@gmail.com** is the default. In the repository's issues (the **Bug report** form) the symptom alone is enough. Send diagnostics bundles and security problems by mail rather than in an issue.
- Good to include: DAC and output mode · what you were doing when, and what you heard. The app version and macOS version are already in the mail form and the bundle.

Step by step: [Task guide §30](HOW-TO.md#30-get-the-beta-and-report-a-problem).
