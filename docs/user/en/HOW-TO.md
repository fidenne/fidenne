<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/HOW-TO.md -->

# Fidenne task guide — "To do something"

Each task is **steps → how to tell it worked**. If it does not work, see the [Troubleshooting guide](TROUBLESHOOTING.md); for what each page contains, the [User manual](MANUAL.md) (the **More** at the end of each section); for the reasons, the [Explanations](EXPLANATIONS.md).
Screen locations are written as `Page › Section › Control`. Pages are chosen in the sidebar (⌘1 Music (음악) · ⌘2 Library (보관함) · ⌘3 Listening History (청취 기록) · ⌘4 DSP · ⌘5 I/O · Diagnostics (입출력 · 진단)). Open Settings (설정) with ⌘,. [Dev build] marks something that exists only in the personal build.

**Contents** — Listening: [1](#1-listen-to-apple-music-and-spotify-through-fidenne) · [2](#2-capture-only-a-specific-apps-sound) · [3](#3-listen-to-music-files-on-this-mac) · [26](#26-play-youtube-music-tracks-from-the-music-page) · [27](#27-search-once-add-a-track-that-is-not-in-your-library-to-the-apple-music-library-and-play-it) · [28](#28-continue-a-track-started-in-the-music-app-in-fidennes-queue) · Output: [4](#4-change-the-output-device-dac) · [5](#5-change-the-output-format--dsd--pcm-integer--pcm-direct) · [6](#6-pick-a-filter-and-dsd-conversion-and-save-it-as-a-sound-preset) · Shaping the sound: [7](#7-load-a-headphone-measurement-and-target) · [8](#8-auto-eq-for-your-headphones) · [9](#9-build-an-eq-by-hand-apply-it-and-save-it) · [10](#10-fix-excessive-settings-boost--clipping) · [11](#11-shape-bass--presence--width-with-ostrum) · [12](#12-reduce-the-left-right-separation-in-headphones--crossfeed) · Comparing: [14](#14-compare-at-the-same-volume-with-ab) · [15](#15-test-blind-whether-you-can-really-hear-a-difference--abx) · [16](#16-alternate-on-and-off-automatically--auto-bypass--loop) · Other: [17](#17-view-lyrics) · [18](#18-view-and-export-listening-history) · [19](#19-turn-off-what-goes-out-to-the-internet) · [20](#20-send-a-support-file-when-something-goes-wrong) · [21](#21-adjust-sliders-and-playback-position-with-two-fingers) · [22](#22-read-feature-and-graph-explanations-in-detail) · [23](#23-check-whether-a-new-version-is-out) · [24](#24-volume-notice-before-sound-starts--turning-output-monitoring-on-and-off) · [25](#25-see-and-control-youtube-music-chrome-from-fidenne) · [29](#29-connect-spotify-for-the-first-time-your-own-key) · [30](#30-get-the-beta-and-report-a-problem)

## 1. Listen to Apple Music and Spotify through Fidenne
1. In `I/O · Diagnostics (입출력 · 진단) › Input and output devices (입력과 출력 장치) › Input (입력)`, choose **Fidenne Inlet** (if missing, **Install… (설치…)** in the same section, one administrator password) or **Process Tap**. For another loopback app, use **+ Another input device (+ 다른 입력 장치)**.
2. In the output DAC picker of the same section, choose the DAC (refresh ↻ if it is not shown).
3. In `I/O · Diagnostics (입출력 · 진단) › Streaming app autoplay (스트리밍 앱 자동 재생) › After the engine starts (엔진 시작 후)`, choose **Auto-detect (자동 감지)** · **Apple Music** · **Spotify** · **YouTube Music (browser) (YouTube Music(브라우저))**. Optional: with Fidenne Inlet as input, turn on **Auto-apply Apple Music source rate (Apple Music 원본 레이트 자동 적용)** to follow the source rate.
4. Turn on the **engine switch (엔진 스위치)** on the bottom playback bar (allow the audio recording · automation macOS asks about the first time) and start a track in the playback app.

**How to tell it worked**: The status text on the bar says "Running (실행 중)" and the source · input · device rows of the **Playback Chain** match what you chose. More: Manual [§7.3](MANUAL.md#73-streaming-app-autoplay--input-and-output-devices) · [§3](MANUAL.md#3-music-page).

## 2. Capture only a specific app's sound
1. Personal build: with Process Tap as the input, choose **Apple Music** · **Spotify** · **Other app (다른 앱)** in `I/O · Diagnostics (입출력 · 진단) › Input and output devices (입력과 출력 장치) › Tap target (탭 대상)`. In the release build, send that app's output to Fidenne Inlet and set the input to Inlet.
2. If the engine is running, turn it off and on — the choice applies from the next start.

**How to tell it worked**: You do not hear that app's original output, only the engine's sound. More: Manual [§7.3](MANUAL.md#73-streaming-app-autoplay--input-and-output-devices).

## 3. Listen to music files on this Mac
1. In `Library (보관함)`, use **Add folder… (폴더 추가…)** (or the **Music folders (음악 폴더)** menu) to choose a music folder and wait for indexing (again: **Music folders (음악 폴더) › Re-index (다시 색인)**).
2. Find a track with the search field and double-click it, or ⋯ → **Play next (다음에 재생)** / **Add to end of queue (대기열 끝에 추가)**. For a playlist, enter a name in **New playlist name (새 재생 목록 이름)** → **Create (만들기)**.
3. Reorder by dragging rows (select several with ⌘-click · Shift-click; play with Return).
4. Optional: to import a YouTube Music playlist, choose the Google Takeout folder with **Import YouTube Music playlists… (YouTube Music 재생목록 가져오기…)** in **YouTube Music library (YouTube Music 보관함)** at the bottom of `Music › YouTube Music › My playlists (내 재생목록)`.

**How to tell it worked**: The track appears on the bar and the Playback Chain source is the file. More: Manual [§4 Library](MANUAL.md#4-library-page) · [§4.1](MANUAL.md#41-importing-youtube-music-playlists).

## 4. Change the output device (DAC)
1. Choose it in the output DAC picker of `I/O · Diagnostics (입출력 · 진단) › Input and output devices (입력과 출력 장치)` (with PCM Direct, `Output mode (출력 방식) › Output DAC (출력 DAC)`). If it is playing, the app reopens the output.
2. Stop the engine before moving the same USB DAC to another port.
3. Optional: to resume when the DAC drops out briefly and returns, turn on `I/O · Diagnostics (입출력 · 진단) › DAC format check (DAC 형식 확인) › Resume playback if the DAC reconnects within 30 seconds (DAC가 30초 안에 다시 연결되면 이어서 재생)`.

**How to tell it worked**: The device row of the Playback Chain shows the new device name. More: Manual [§7.2](MANUAL.md#72-dac-format-check-formerly-engine-output-format) · [§7.3](MANUAL.md#73-streaming-app-autoplay--input-and-output-devices).

## 5. Change the output format — DSD · PCM integer · PCM Direct
1. In `I/O · Diagnostics (입출력 · 진단) › Output mode (출력 방식)` (or the output mode menu on the bar), choose **DSD (DoP)** · **PCM 352.8 kHz** · **PCM Direct**.
2. For PCM 352.8 kHz, also choose **PCM bit depth (PCM 비트 깊이)** (24 · 16-bit) and **Dither (디더)** below it.
3. Lower the DAC volume before switching to PCM Direct — the engine's headroom is not applied.
4. Changing while stopped is the most reliable; during playback it says "Applies from the next start (다음 시작부터 적용됩니다)".

**How to tell it worked**: The output row of the Playback Chain shows the chosen format and the `DAC format check (DAC 형식 확인)` table shows **Confirmed (확인됨)** (✓). To see beforehand what the DAC accepts, stop playback and press **Check all (모두 확인)**. More: Manual [§7.1](MANUAL.md#71-independent-output-control--output-mode) · [§7.2](MANUAL.md#72-dac-format-check-formerly-engine-output-format).

## 6. Pick a filter and DSD conversion, and save it as a sound preset
1. On the `I/O · Diagnostics (입출력 · 진단) › Filter · Modulator · Output gain (필터 · 모듈레이터 · 출력 게인)` card (the bar's output mode menu → **Sound settings… (사운드 설정…)** comes here too), press a **Suggested combination (추천 조합)** under **Where should I start listening? (어디서부터 들어볼까요?)**. To choose directly, use **Processing method (처리 방식)** · **Family (계열)** · **Length (길이)**; to choose by cost, **Choose by conditions · cost comparison (조건으로 고르기 · 비용 비교)**.
2. For DSD conversion choose **Modulator (모듈레이터)** · **Output rate (출력 레이트)** · **Buffer (버퍼)** (only while stopped). Leave PCM headroom on **Auto (recommended) (자동 (권장))**.
3. Press "Save current sound preset (현재 사운드 프리셋 저장)" — it appears under "Saved presets (저장한 프리셋)" in the bar's output mode menu, and choosing it restores the saved engine output (DSD, or PCM depth · 352.8 kHz). PCM Direct is not saved.

**How to tell it worked**: The filter · output rows of the Playback Chain show what you chose. More: Manual [§7.4](MANUAL.md#74-filter--modulator--output-gain-card--sound-settings-for-the-dsd-path).

## 7. Load a headphone measurement and target
1. In `DSP › Equalizer`, open **Headphone ▾** on the **Auto EQ** row (right before the band columns). Choose a favorited headphone right away.
2. Otherwise **Search headphones… (헤드폰 검색…)** (the first time, **Get list (목록 받기)**), enter a name, press the result and **Apply (적용)**. Favorite with the ☆ at the start of a row.
3. For the target use **Target ▾**: **Target curves (타깃 곡선)** (DF · DF t · Harman …) or **Target headphone favorites (목표 헤드폰 즐겨찾기)**. For files, **Open measurement file… (측정 파일 열기…)** · **Open target file… (타깃 파일 열기…)**.

**How to tell it worked**: The Headphone · Target layers of the Response graph are drawn and both menus show the names (the sound does not change). The squig.link network destination must be on ([19](#19-turn-off-what-goes-out-to-the-internet)). More: Manual [§6.5](MANUAL.md#65-headphone---target--the-auto-eq-row-of-equalizer--advanced--files--treble--generative-ai-collapsible).

## 8. Auto EQ for your headphones
1. Set the measurement and target as in section 7.
2. In `DSP › Equalizer › Auto EQ`, choose the number of bands in **Bands** (default 10) and press **Auto fit**. You hear the result immediately.
3. For a weaker effect lower **Strength**; if a narrow ripple remains, raise Bands to 12–16 and Auto fit again.
4. If you like it, press **Save (저장)** in the header (⌘S). One step back is ⌘Z; back to the saved one is **Revert to saved (저장본으로 되돌리기)**.

**How to tell it worked**: The header says "Matches the engine settings (엔진 설정과 일치)" · "✓ Saved (✓ 저장됨)" and the **After correction (보정 뒤)** line sticks to the dotted **Target** line. If the detector warns, go to section 10. More: Manual [§6.6](MANUAL.md#66-bands--strength--auto-fit-the-auto-eq-row-of-equalizer--what-auto-fit-did-collapsible).

## 9. Build an EQ by hand, apply it, and save it
1. In `DSP › Equalizer`, turn on **EQ On**.
2. Drag a band column's slider or the blue point on the graph, or type in the type · Gain · Freq · Q fields (confirm with Return). You hear each change immediately. Add a band with **Add Band**, use 31 bands with **Graphic 31**, and open a text preset with **Open EQ Preset…**.
3. To start over use **Reset (초기화)**, to return to the saved one **Revert to saved (저장본으로 되돌리기)**, and for one step ⌘Z.
4. Press **Save (저장)** (⌘S) — the EQ you hear is saved together with the Headphone · Target on screen **into the current preset** (the name in the header) and used from the next launch. Changing only the Headphone · Target turns Save on too. To keep it under a new name, **Save as… (다른 이름으로 저장…)**. Earlier ones are in **Revert to previous saved version (이전 저장본으로 되돌리기)**.

**How to tell it worked**: The header says "Matches the engine settings (엔진 설정과 일치)" · "✓ Saved (✓ 저장됨)", and the same bands are there after a restart. More: Manual [§6.2](MANUAL.md#62-equalizer).

## 10. Fix excessive settings (boost · clipping)
1. When "Detector: excessive settings (탐지기: 과한 설정 있음)" appears under the Response graph, press **Correction suggestions… (보정 제안…)**.
2. Choose the **Correction method (보정 방법)** (industry convention or improved), look at the table of bands that will change and press **Apply correction (보정 적용)**. To undo, the detector's **ⓘ › Undo correction (보정 되돌리기)**.
3. To only prevent clipping, turn on **ⓘ › Prevent clipping — lower Preamp automatically (클리핑 막기 — Preamp 자동 낮춤)**. If it clips during playback, check that PCM headroom is **Auto**; if so, use **Apply Headroom N dB** in `Equalizer › Clipping & Headroom` or **Turn Limiter On**.

**How to tell it worked**: The detector says "No excessive settings (과한 설정 없음)" and Clipping & Headroom says "No output-stage clipping in this playback (이 재생에서 출력 단 클리핑 없음)". More: Manual [§6.2](MANUAL.md#62-equalizer) · [§6.1](MANUAL.md#61-response-graph).

## 11. Shape bass · presence · width with Ostrum
1. In `DSP › Ostrum`, turn on **Ostrum On**. Everything you move is heard immediately.
2. Start with **Presets ▾ → Natural (자연스럽게)** in the header. By hand, set **Tune** and raise **Mix** (with Mix 0, Bass · Presence are inaudible).
3. Adjust Bass · Presence · Width while listening. If Harmonics is on, press **Set Headroom to the recommended value (권장값으로 Headroom 맞추기)**. To hear Presence **Linear Phase** now, press **Restart Now**.
4. Press **Save (저장)** (⌘S). To discard, **Revert to saved (저장본으로 되돌리기)**. For several sets, **Presets ▾ → Save current settings as my preset… (지금 설정을 내 프리셋으로 저장…)**.

**How to tell it worked**: The header shows `✓ Saved (✓ 저장됨)` and "Applied · revision N (적용됨 · 리비전 N)", and the Ostrum layer of the Response graph moves away from 0 dB. For an on/off comparison see section 16. More: Manual [§6.3](MANUAL.md#63-ostrum).

## 12. Reduce the left-right separation in headphones — crossfeed
1. In `DSP › Crossfeed`, turn on **Turn crossfeed on (크로스피드 켜기)**.
2. Try **Light · Medium · Strong (가볍게 · 보통 · 진하게)**, then adjust with the **Amount (양)** and **Frequency (주파수)** knobs.
3. Save a value you like under a name with **My settings (내 설정) › Save current values… (지금 값을 저장…)**.

**How to tell it worked**: During playback, Side in the M/S window goes down (Mid stays at 0.00 dB). More: Manual [§6.4](MANUAL.md#64-crossfeed).

## 14. Compare at the same volume with A/B
1. Press the **A/B** button at the end of the DSP header to open the panel, **Save Current to A** with the first setting, change the setting and **Save Current to B**.
2. **Start A/B**, then alternate with `Request Slot A` / `Request Slot B`. Check that **Level Match** is on. To finish, End Comparison.

**How to tell it worked**: The header button states the current side, as in `A/B · listening to B (A/B · B 듣는 중)`. More: Manual [§6.7](MANUAL.md#67-the-ab-buttons-panel--ab--abx--auto-bypass--loop--level-matched-comparison-음량-맞춤).

## 15. Test blind whether you can really hear a difference — ABX
1. Save A · B and start as in section 14. In ABX in the panel, set **Trials** (default 16) before starting.
2. **Start ABX**, listen to X and choose **X is A** / **X is B**. To quit, **Stop (no verdict)**.

**How to tell it worked**: When it ends, the number correct and the verdict are shown and "Recent Runs on This Mac" gets a line. More: Manual [§6.7](MANUAL.md#67-the-ab-buttons-panel--ab--abx--auto-bypass--loop--level-matched-comparison-음량-맞춤).

## 16. Alternate on and off automatically — Auto Bypass · Loop
1. After turning Ostrum on and applying it, press **Start Auto Bypass** in the A/B panel. Set the interval with **Switch Interval** (2–30 s).
2. For the section you just heard, while playing a library file, set **Look-back** and press **Start Loop Comparison**.

**How to tell it worked**: The "current side (현재 쪽)" on the bar changes at each interval. More: Manual [§6.7](MANUAL.md#67-the-ab-buttons-panel--ab--abx--auto-bypass--loop--level-matched-comparison-음량-맞춤).

## 17. View lyrics
1. Play a track and on the bar use ⋯ → **View lyrics (가사 보기)**.
2. The first time, choose **Agree and search (동의하고 찾기)** (only the title · artist · album · length are sent), or **Do not send (보내지 않음)** and attach an LRC · TXT file.
3. Adjust timing with + / −, text size in `Settings (설정) › Display (화면) › Lyrics text size (가사 글자 크기)`, and other editions with the book-shaped **Lyrics edition (가사 판)** or **Find other editions (다른 판 찾기)**.

**How to tell it worked**: The lyrics appear in the lyrics panel. More: Manual [§2.3](MANUAL.md#23-lyrics).

## 18. View and export listening history
1. In `Listening History (청취 기록)`, choose the **Recent (최근)** period and the **Source (출처)**.
2. **Export (내보내기)** → **JSON · includes counting criteria (JSON · 집계 기준 포함)** or **CSV · 1 row = 1 play (CSV · 1행 = 재생 1회)**.
3. To stop recording, turn off **Recording settings and counting criteria (기록 설정과 집계 기준) › Save listening history on this Mac (이 Mac에 청취 기록 저장)**.

**How to tell it worked**: The plays of the period · source you chose appear in the graph and the per-track history. More: Manual [§5](MANUAL.md#5-listening-history-page).

## 19. Turn off what goes out to the internet
1. In `Settings (설정) › Privacy (개인정보) › Network destinations (네트워크 목적지)`, turn off each destination.
2. To turn off only lyrics, `Settings (설정) › Privacy (개인정보) › Lyrics internet search (가사 인터넷 검색) › Look for lyrics on lrclib.net (lrclib.net에서 가사 찾기)`.

**How to tell it worked**: Even with everything off, capture · DSP · DSD conversion · DAC output · local playback work. More: Manual [§8](MANUAL.md#8-settings-window).

## 20. Send a support file when something goes wrong
1. **Help → Create diagnostics for a problem report… (도움말 → 문제 제보용 진단 만들기…)**. If recording is off, **Start diagnostic recording (진단 기록 시작)** → reproduce the problem → **Stop diagnostic recording (진단 기록 정지)**. [Dev build]: at the moment the problem happens, **Mark problem occurred (문제 발생 표시)** in the Diagnostics menu.
2. **Create bundle and view contents (번들 만들고 내용 보기)** and check the contents (they include the title · artist · service of songs you listened to).
3. Press **Send by mail (메일로 보내기)**; when the mail app opens, compress the folder and attach it. Send the diagnostic bundle by mail only — do not put it on a GitHub issue.

**How to tell it worked**: The folder opened with **Open bundle folder (번들 폴더 열기)** has `support.json` · `manifest.json` · `tracks.json` · `README.txt`. More: Manual [§10](MANUAL.md#10-sending-a-support-file).

## 21. Adjust sliders and playback position with two fingers
1. Put the pointer over a control (playback position · EQ gain · Ostrum knob · PCM headroom slider, and so on).
2. **Hold ⌘** and swipe up with two fingers to go up and down to go down (add ⌥ or Shift to go slowly). The playback position moves once when you lift your hand.
3. To keep an EQ change, save (⌘S). For a graph point, first press it to select it, then swipe.

**How to tell it worked**: The number next to the control changes while you swipe. If it does not, check `Settings (설정) › Controls and shortcuts (조작과 단축키) › Change values with two-finger scroll (두 손가락 스크롤로 값 바꾸기)`. More: Manual [§2.6](MANUAL.md#26-handling-knobs--sliders--eq-points).

## 22. Read feature and graph explanations in detail
1. Press the **ⓘ** at the end of the one line under a section title (with the keyboard, Tab then Space). For graphs, the **ⓘ** at the end of the lines row.
2. Read **When do I use it? · What do I put in? · What changes if I change it? · Cost (언제 쓰나요? · 무엇을 넣나요? · 바꾸면 무엇이 달라지나요? · 대가)**; for unknown words use **Glossary (용어 풀이)**. Close with **Esc**.

**How to tell it worked**: The balloon appears right below the ⓘ (hovering alone does not open it). More: Manual [§2.5](MANUAL.md#25-explanations--how-to-read-graphs--glossary).

## 23. Check whether a new version is out
1. Press **Fidenne › Check for updates… (업데이트 확인…)** in the app menu.
2. "Up to date (최신입니다)" means you are done. If there is a new version, press **Install and restart (설치하고 다시 시작)** (Homebrew: **Copy command (명령 복사)**; .dmg: **Open release page (릴리스 페이지 열기)**).
3. Optional: turn on **Check for a new version automatically once a day (새 버전을 하루에 한 번 자동으로 확인)** at the bottom of `Settings (설정) › Privacy (개인정보) › Network destinations (네트워크 목적지)`.

**How to tell it worked**: "Current version (지금 판)" in the result window matches the version on the top row of the Settings window. More: Manual [§8](MANUAL.md#8-settings-window).

## 24. Volume notice before sound starts · turning output monitoring on and off
1. In **Start with the volume lowered (음량을 낮추고 시작하세요)**, which appears at the first play, lower the DAC · amp volume and press **Lowered it, start (낮췄어요, 시작)**. Raise the volume slowly.
2. To stop the notice every time, turn off `Settings (설정) › Sound safety (소리 안전) › Volume notice every time it turns on (켤 때마다 음량 안내)` (a DAC you use for the first time still shows it once).
3. Keep `Settings (설정) › Sound safety (소리 안전) › Mute when a signal not in the music appears (음악에 없는 신호가 나오면 음소거)` on.

**How to tell it worked**: Playback starts and there is no mute row at the head of the window. More: Manual [§1](MANUAL.md#1-first-launch--the-four-step-first-run-setup) · [§8](MANUAL.md#8-settings-window).

## 25. See and control YouTube Music (Chrome) from Fidenne
1. Turn on `Settings (설정) › Privacy (개인정보) › YouTube Music › Connect with Chrome · Edge extension (Chrome · Edge 확장과 연결)`, and in **Setup guide… (설치 안내…)** choose **Chrome** or **Edge**.
2. Follow the guide window — **Copy address (주소 복사)** → paste it in the address bar and press Return → turn on **Developer mode (개발자 모드)** → **Load unpacked (압축해제된 확장 프로그램을 로드합니다)** → **Copy path (경로 복사)** → in the file window ⌘⇧G · ⌘V · Return · **Open (열기)**.
3. Reload the YouTube Music tab that was already open with ⌘R and play a track.
4. A browser that puts unused tabs to sleep leaves YouTube Music unable to answer — add `music.youtube.com` as an exception: Chrome under Settings → Performance → Memory Saver → **Always keep these sites active**, Edge under Settings → System and performance → Resource controls → **Never put these sites to sleep**.

**How to tell it worked**: The line under the guide window says `1 browser connected (브라우저 1개 연결됨)` and the bar shows that track and "YouTube Music (browser) (YouTube Music (브라우저))". After updating the app, press ↻ once on the **Fidenne for YouTube Music** card in `chrome://extensions` (Edge `edge://extensions`) and reload the tab with ⌘R. More: Manual [§8.1](MANUAL.md#81-using-youtube-music-chrome-extension).

## 26. Play YouTube Music tracks from the Music page
1. Press the service button before the Music page's search field and choose **YouTube Music**. If it says "Not connected (연결 안 됨)", do section 25.
2. In **My playlists (내 재생목록)**, open a list and press **Play all (전체 재생)** (or one track). If there is no list, open that screen once in YouTube Music — within a few seconds it appears as `From browser (브라우저에서)`.
3. To search, type in **Search in YouTube Music (YouTube Music 에서 검색)** and press Return.

**How to tell it worked**: The status row says `Playing in Chrome (Chrome 에서 재생 중)` and the track and the previous · play · next buttons appear. More: Manual [§8.1](MANUAL.md#81-using-youtube-music-chrome-extension) · [§3](MANUAL.md#3-music-page).

## 27. Search once, add a track that is not in your library to the Apple Music library, and play it
1. On the Music page, set the service to **Apple Music**, type in the search field and press Return. Results run **Apple Music** (my library) → **Apple Music catalog (Apple Music 카탈로그)** → **Local library (로컬 보관함)**.
2. On a catalog row press **Add to library (보관함에 추가)** and, in the confirmation the first time, **Add (추가)**.
3. The row changes to `Added · appearing in the library (추가했습니다 · 보관함에 나타나는 중)`, then its button becomes **Play (재생)** — press it. Spotify results are under the **Spotify** tab at the top.

**How to tell it worked**: The added track also shows in the Music app's library. More: Manual [§3](MANUAL.md#3-music-page).

## 28. Continue a track started in the Music app in Fidenne's queue
1. Start a track in the Music app. Press the cover on Fidenne's bottom playback capsule to open the large playback view; the following tracks appear in **Up next (다음 재생)**.
2. To let Fidenne decide the order, use ⋯ on a track row → **Play next (다음에 재생)** · **Add to end of queue (대기열 끝에 추가)**, or the bar's shuffle · repeat.
3. If three buttons appear, choose **Continue this album (이 앨범 이어 듣기)** · **Return to Fidenne's list (Fidenne 목록으로 돌아가기)** · **Leave it to Apple Music autoplay (Apple Music 자동 재생에 맡기기)**.

**How to tell it worked**: When a track ends, the next one in Up next follows. More: Manual [§2.2](MANUAL.md#22-bottom-playback-bar).

## 29. Connect Spotify for the first time (your own key)
1. In the Spotify section of Settings, press **Open developer dashboard (개발자 대시보드 열기)** and create an app in the Spotify developer dashboard.
2. Put the address shown in the field into that app's Redirect URI (the **Copy (복사)** button beside it copies it).
3. Paste the dashboard's **Client ID** into Fidenne's field (do not enter the Client Secret).
4. Press **Check key (키 확인)**, then **Connect Spotify (Spotify 연결)** and allow it in the login window.

**How to tell it worked**: Searching with Spotify in the Music page's service list returns results, and Settings has **Refresh playback permission (재생 권한 갱신)** · **Disconnect (연결 해제)**. Without a key, sound processing of tracks played in the Spotify app still works. More: Manual [§3](MANUAL.md#3-music-page).

## 30. Get the beta and report a problem
1. Get the signed and notarized `.dmg` from the releases page (`https://github.com/fidenne/fidenne/releases`) (Apple silicon Mac, macOS 26 or later).
2. Make a support file as in section 20 and send it to **fidenne.support@gmail.com** (**Send by mail (메일로 보내기)** fills it in).
3. Write the app version · macOS version · DAC and output mode · what you were doing and what you heard or saw. Send security problems by mail instead of a public issue.

**How to tell it worked**: The mail has the above and the support file. The app sends nothing on its own. More: Manual [§10](MANUAL.md#10-sending-a-support-file).
