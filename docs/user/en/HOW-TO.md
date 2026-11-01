<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/HOW-TO.md (0.7.0 edition) -->

# Fidenne task guide — "To do something"

Each task is **steps → how to tell it worked**. If it does not work, see the [Troubleshooting guide](TROUBLESHOOTING.md); for what each page contains, the [User manual](MANUAL.md) (the **More** at the end of each section); for why things work the way they do, the [Explanations](EXPLANATIONS.md).
Screen locations are written as `Page › Section › Control`. Pages are chosen in the sidebar (⌘1 Streaming (스트리밍) · ⌘2 Local (로컬) · ⌘3 Listening History (청취 기록) · ⌘4 EQ · ⌘5 I/O · Diagnostics (입출력 · 진단)). Open Settings (설정) with ⌘,.
For what cannot be done, see [Known limitations](KNOWN_LIMITATIONS.md).

**Contents** — Listening: [1](#1-listen-to-apple-music-and-spotify-through-fidenne) · [2](#2-capture-only-a-specific-apps-sound) · [3](#3-listen-to-music-files-on-this-mac) · [26](#26-play-youtube-music-tracks-from-the-streaming-page) · [27](#27-search-once-add-a-track-that-is-not-in-your-library-to-the-apple-music-library-and-play-it) · [28](#28-continue-a-track-started-in-the-music-app-in-fidennes-queue) · Output: [4](#4-change-the-output-device-dac) · [5](#5-change-the-output-format--dsd--pcm-integer--pcm-direct) · [6](#6-pick-a-filter-and-dsd-conversion-and-save-it-as-a-sound-preset) · Shaping the sound: [7](#7-load-a-headphone-measurement-and-target) · [8](#8-auto-eq-for-your-headphones) · [9](#9-build-an-eq-by-hand-apply-it-and-save-it) · [10](#10-fix-excessive-settings-boost--clipping) · [11](#11-shape-bass--presence--width-with-ostrum) · [12](#12-reduce-the-left-right-separation-in-headphones--crossfeed) · [13 IR](#13-apply-a-measured-headphone--speaker--room-response--ir-convolution) · Comparing: [14](#14-compare-at-the-same-volume-with-ab) · [15](#15-test-blind-whether-you-can-really-hear-a-difference--abx) · [16](#16-alternate-on-and-off-automatically--auto-bypass--loop) · Other: [17](#17-view-lyrics) · [18](#18-view-and-export-listening-history) · [19](#19-turn-off-what-goes-out-to-the-internet) · [20](#20-send-a-support-file-when-something-goes-wrong) · [21](#21-adjust-sliders-and-playback-position-with-two-fingers) · [22](#22-read-feature-and-graph-explanations-in-detail) · [23](#23-check-whether-a-new-version-is-out) · [24](#24-volume-notice-before-sound-starts--turning-output-monitoring-on-and-off) · [25](#25-see-and-control-youtube-music-chrome-from-fidenne) · [29](#29-connect-spotify-for-the-first-time-your-own-key) · [30](#30-get-the-beta-and-report-a-problem) · 0.6: [31](#31-use-youtube-music-in-safari) · [32](#32-save-an-album-to-your-library) · [33](#33-reorder-songs-your-way) · [34](#34-translate-lyrics-with-ai) · [35](#35-change-the-loudness-with-the-dac-volume-slider) · [36](#36-when-fidenne-stops-while-opening) · 0.7: [37 Output rate](#37-choose-the-pcm-output-rate--follow-the-sources-rate-family) · [38 Between songs](#38-choose-how-songs-join--when-the-dac-cuts-the-first-sound) · [39 Speakers and AirPods](#39-process-built-in-speakers--airpods--hdmi-with-fidenne) · [40 Plug-ins](#40-put-an-audio-unit-plug-in-in-the-path) · [41 EQ import](#41-import-an-eq-file-rew--equalizer-apo--autoeq) · [42 Home drag](#42-add-songs-to-a-playlist-group-them-and-remove-them-from-history-on-home) · [43 Shortcuts](#43-call-play-and-bypass-of-sound-processing-from-shortcuts) · [44 Pronunciation line](#44-turn-on-the-lyrics-pronunciation-line-and-reorder-the-lines) · [45 Sleep timer](#45-sleep-timer-and-volume-keys) · [46 Language](#46-use-the-screens-in-english-or-japanese)

## 1. Listen to Apple Music and Spotify through Fidenne
1. In `I/O · Diagnostics (입출력 · 진단) › Advanced (고급) › Input (소리 받기)`, choose **Fidenne Inlet** (if missing, **Install… (설치…)** in the same section, one administrator password) or **Process Tap**, which receives system sound without an install. For another loopback app, use **+ Another input device (+ 다른 입력 장치)**.
2. In the output DAC picker of the same section, choose the DAC (refresh ↻ if it is not shown).
3. In `I/O · Diagnostics (입출력 · 진단) › Advanced (고급) › Streaming app autoplay (스트리밍 앱 자동 재생) › After the engine starts (엔진 시작 후)`, choose **Auto-detect (자동 감지)** · **Apple Music** · **Spotify** · **YouTube Music (browser) (YouTube Music(브라우저))**. Optional: with Fidenne Inlet as input, turn on **Auto-apply Apple Music source rate (Apple Music 원본 레이트 자동 적용)** to follow the source rate.
4. Turn on the **engine switch (엔진 스위치)** on the bottom playback bar (allow the audio recording · automation macOS asks about the first time) and start a track in the playback app.

**How to tell it worked**: The status text on the bar says "Running (실행 중)" and the source · input · device rows of the **Playback Chain** match what you chose. More: Manual [§7.3](MANUAL.md#73-streaming-app-autoplay--input-and-output-devices) · [§3](MANUAL.md#3-streaming-page).

## 2. Capture only a specific app's sound
1. In this version the system tap (Process Tap) takes **the whole system** only. To take only one app's sound, send that app's output to **Fidenne Inlet** (System Settings › Sound › Output, or the app's own output-device setting) and set `I/O · Diagnostics (입출력 · 진단) › Advanced (고급) › Input (소리 받기)` to **Fidenne Inlet**.
2. If the engine is running, turn it off and on — the choice applies from the next start.

**How to tell it worked**: You do not hear that app's original output, only the engine's sound. More: Manual [§7.3](MANUAL.md#73-streaming-app-autoplay--input-and-output-devices).

## 3. Listen to music files on this Mac
1. In `Local (로컬)`, use **Add folder… (폴더 추가…)** (or the **Music folders (음악 폴더)** menu) to choose a music folder and wait for indexing (again: **Music folders (음악 폴더) › Re-index (다시 색인)**).
2. Find a track with the search field and double-click it, or ⋯ → **Play next (다음에 재생)** / **Add to end of queue (대기열 끝에 추가)**. For a playlist, enter a name in **New playlist name (새 재생목록 이름)** → **Create (만들기)**.
3. Reorder by dragging rows (select several with ⌘-click · Shift-click; play with Return).
4. Optional: to import a YouTube Music playlist, choose the Google Takeout folder with **Import YouTube Music playlists… (YouTube Music 재생목록 가져오기…)** in **YouTube Music library (YouTube Music 보관함)** at the bottom of `Streaming › YouTube Music › My playlists (내 재생목록)`.

**How to tell it worked**: The track appears on the bar and the Playback Chain source is the file. More: Manual [§4 Library](MANUAL.md#4-local-page) · [§4.1](MANUAL.md#41-importing-youtube-music-playlists).

## 4. Change the output device (DAC)
1. Choose it in the output DAC picker of `I/O · Diagnostics › Output device`. PCM Direct allows switching during playback. Stop the engine before changing the device while engine processing is running.
2. Stop the engine before moving the same USB DAC to another port.
3. Optional: to resume when the DAC drops out briefly and returns, turn on `I/O · Diagnostics (입출력 · 진단) › Advanced › Reconnect DAC › Resume if reconnected within 30 seconds`.

**How to tell it worked**: The device row of the Playback Chain shows the new device name. More: Manual [§7.2](MANUAL.md#72-dac-format-check-formerly-engine-output-format) · [§7.3](MANUAL.md#73-streaming-app-autoplay--input-and-output-devices).

## 5. Change the output format — DSD · PCM integer · PCM Direct
1. In `I/O · Diagnostics (입출력 · 진단) › Output mode (출력 방식)` (or the output mode menu on the bar), choose **PCM Direct** · **PCM oversampling (PCM 오버샘플)** · **DSD**.
2. For PCM oversampling, `Advanced › PCM` also has the **Output rate** (a new configuration keeps the source rate — see section [37](#37-choose-the-pcm-output-rate--follow-the-sources-rate-family)), **Bit depth (비트 깊이)** (24 · 16-bit) and **Dither (디더)**.
3. Lower the DAC volume before switching to PCM Direct — the engine's headroom is not applied.
4. Changing while stopped is the most reliable; during playback it says "Applies from the next start (다음 시작부터 적용됩니다)".

**How to tell it worked**: The output row of the Playback Chain shows the chosen format and the `DAC format check (DAC 형식 확인)` table shows **Confirmed (확인됨)** (✓). To see beforehand what the DAC accepts, stop playback and press **Check all (모두 확인)**. More: Manual [§7.1](MANUAL.md#71-independent-output-control--output-mode) · [§7.2](MANUAL.md#72-dac-format-check-formerly-engine-output-format).

## 6. Pick a filter and DSD conversion, and save it as a sound preset
1. On the `I/O · Diagnostics › Advanced › Filter` row (the bar's output mode menu → **Sound settings… (사운드 설정…)** comes here too), press a **Suggested combination (추천 조합)** under **Where should I start listening? (어디서부터 들어볼까요?)**. To choose directly, use **Processing method (처리 방식)** · **Family (계열)** · **Length (길이)**; to choose by cost, **Choose by conditions · cost comparison (조건으로 고르기 · 비용 비교)**.
2. For DSD conversion choose **Conversion method** and **Output rate** under **Advanced › DSD conversion** (only while stopped). Leave PCM headroom on **Auto (recommended) (자동 (권장))**.
3. Press **Save current settings as preset… (지금 설정을 프리셋으로 저장…)** — it appears under "Saved presets (저장한 프리셋)" in the bar's output mode menu, and choosing it restores the saved engine output (DSD, or PCM depth · output rate). PCM Direct is not saved.

**How to tell it worked**: The filter · output rows of the Playback Chain show what you chose. More: Manual [§7.4](MANUAL.md#74-filter--modulator--output-gain-card--sound-settings-for-the-dsd-path).

## 7. Load a headphone measurement and target
1. In `DSP › EQ`, open **My headphones (내 헤드폰)** on the **Auto EQ** row (right before the band columns). Choose a favorited headphone right away.
2. Otherwise **Search headphones… (헤드폰 검색…)** (the first time, **Get list (목록 받기)**), enter a name, press the result and **Apply (적용)**. Favorite with the ☆ at the start of a row.
3. For the target use **Target (목표)**: **Target curves (타깃 곡선)** (DF · DF t · Harman …) or **Target headphone favorites (목표 헤드폰 즐겨찾기)**. For files, **Open measurement file… (측정 파일 열기…)** · **Open target file… (타깃 파일 열기…)**.

**How to tell it worked**: The Headphone · Target layers of the Response graph are drawn and both menus show the names (the sound does not change). The squig.link network destination must be on ([19](#19-turn-off-what-goes-out-to-the-internet)). More: Manual [§6.5](MANUAL.md#65-headphone---target--the-auto-eq-row-of-equalizer--advanced--files--treble--generative-ai-collapsible).

## 8. Auto EQ for your headphones
1. Set the measurement and target as in section 7.
2. In `DSP › EQ › Auto EQ`, choose the number of bands in **Bands** (default 10) and press **Apply (적용)**. You hear the result immediately.
3. For a weaker effect lower **Strength**; if a narrow ripple remains, raise Bands to 12–16 and Auto fit again.
4. If you like it, press **Save (저장)** in the header (⌘S). One step back is ⌘Z; back to the saved one is **Revert to saved (저장본으로 되돌리기)**.

**How to tell it worked**: The header says "Matches the engine settings (엔진 설정과 일치)" · "✓ Saved (✓ 저장됨)" and the **After correction (보정 뒤)** line sticks to the dotted **Target** line. If the detector warns, go to section 10. More: Manual [§6.6](MANUAL.md#66-bands--strength--auto-fit-the-auto-eq-row-of-equalizer--what-auto-fit-did-collapsible).

## 9. Build an EQ by hand, apply it, and save it
1. In `DSP › EQ`, turn on **Turn on EQ (EQ 켜기)**.
2. Drag a band column's slider or the blue point on the graph, or type in the type · Gain · Freq · Q fields (confirm with Return). You hear each change immediately. Add a band with **Add band (밴드 추가)**, use 31 bands with **31-band graphic (31밴드 그래픽)**, and open a text preset with **Open EQ preset… (EQ 프리셋 열기…)**.
3. To start over use **Reset (초기화)**, to return to the saved one **Revert to saved (저장본으로 되돌리기)**, and for one step ⌘Z.
4. Press **Save (저장)** (⌘S) — the EQ you hear is saved together with the Headphone · Target on screen **into the current preset** (the name in the header) and used from the next launch. Changing only the Headphone · Target turns Save on too. To keep it under a new name, **Save as… (다른 이름으로 저장…)**. Earlier ones are in **Revert to previous saved version (이전 저장본으로 되돌리기)**.

**How to tell it worked**: The header says "Matches the engine settings (엔진 설정과 일치)" · "✓ Saved (✓ 저장됨)", and the same bands are there after a restart. More: Manual [§6.2](MANUAL.md#62-equalizer).

## 10. Fix excessive settings (boost · clipping)
1. When "Excessive settings found (과한 설정 있음)" appears under the Response graph, press **Correction suggestions… (보정 제안…)**.
2. The window opens on **industry convention (업계 관례)** (lower the Preamp only). Optional: to fix only the overflowing bands, choose **improved (개선)**. Look at the table of bands that will change and press **Apply correction (보정 적용)**. To undo, the detector's **ⓘ › Undo correction (보정 되돌리기)**.
3. To only prevent clipping, turn on **ⓘ › Prevent clipping — lower Preamp automatically (클리핑 막기 — Preamp 자동 낮춤)** (off by default; it lowers only the Preamp and never changes a band). If it clips during playback, check whether PCM headroom is **Auto**; if it is not, use **Apply Headroom N dB** in `Equalizer › Clipping & Headroom` or **Turn Limiter On**.

**How to tell it worked**: The detector says "No excessive settings (과한 설정 없음)" and Clipping & Headroom says "No output-stage clipping in this playback (이 재생에서 출력 단 클리핑 없음)". More: Manual [§6.2](MANUAL.md#62-equalizer) · [§6.1](MANUAL.md#61-response-graph).

## 11. Shape bass · presence · width with Ostrum
1. In `DSP › Ostrum`, turn on **Ostrum On**. Everything you move is heard immediately.
2. Start with **Presets ▾ → Natural (자연스럽게)** in the header. By hand, set **Tune** and raise **Mix** (with Mix 0, Bass · Presence are inaudible).
3. Adjust Bass · Presence · Width while listening. If Harmonics is on, press **Set Headroom to the recommended value (권장값으로 Headroom 맞추기)**. To hear Presence **Linear Phase** now, press **Restart Now**.
4. Press **Save (저장)** (⌘S). To discard, **Revert to saved (저장본으로 되돌리기)**. For several sets, **Presets ▾ → Save current settings as my preset… (지금 설정을 내 프리셋으로 저장…)**.

**How to tell it worked**: The header shows `✓ Saved (✓ 저장됨)` and "Applied · revision N (적용됨 · 리비전 N)", and the Ostrum layer of the Response graph moves away from 0 dB. More: Manual [§6.3](MANUAL.md#63-ostrum).

## 12. Reduce the left-right separation in headphones — crossfeed
1. In `DSP › Crossfeed`, turn on **Turn crossfeed on (크로스피드 켜기)**.
2. Try **Light · Medium · Strong (가볍게 · 보통 · 진하게)**, then adjust with the **Amount (양)** and **Frequency (주파수)** knobs.
3. Save a value you like under a name with **My settings (내 설정) › Save current values… (지금 값을 저장…)**.

**How to tell it worked**: During playback, Side in the M/S window goes down (Mid stays at 0.00 dB). More: Manual [§6.4](MANUAL.md#64-crossfeed).

## 13. Apply a measured headphone · speaker · room response — IR (convolution)

**You need**: a WAV · AIFF IR file (1 · 2 · 4 channels, 44.1–192 kHz). No IRs are included.

1. Open **DSP › Convolution (컨볼루션)** in the sidebar and press **Choose IR File… (IR 파일 고르기…)**.
2. When preparation finishes, check the file information and **Gain (게인)**. A new file uses the lower of the current gain and its suggested gain. For four channels, also check **Channel order (채널 순서)**.
3. Turn on **Turn On (켜기)**.
4. Optional: edit the gain and press **Apply (적용)**. **Suggested value (제안값)** applies the suggested gain immediately. The ceiling uses the full-band response, including 0 Hz.
5. Optional: while the IR is being applied, turn on **Compare without the IR, at the same latency (IR 없이 같은 지연으로 비교)**. To turn the IR off, turn off **Turn On (켜기)**.

**How to tell it worked**: During playback, the panel shows **IR active (IR 적용 중)** and the actual latency, and the Playback Chain's PCM-A chain shows convolution. Latency increases by about 24–49 ms. When replacing a file, the previous IR stays in use during preparation, so check the processing state.

**If it does not work**: Check the panel's notice and gain ceiling.

## 14. Compare at the same volume with A/B
A/B comparison is **hidden in this beta** — the DSP page has no A/B button. It comes back once it is fixed. More: [Known limitations](KNOWN_LIMITATIONS.md#left-out-of-beta-1).

## 15. Test blind whether you can really hear a difference — ABX
The ABX test is **hidden in this beta** too (for the same reason as A/B). More: [Known limitations](KNOWN_LIMITATIONS.md#left-out-of-beta-1).

## 16. Alternate on and off automatically — Auto Bypass · Loop
Auto Bypass · Loop comparison is **hidden in this beta** too. To compare on and off, press that feature's on switch on the DSP page yourself and listen. More: [Known limitations](KNOWN_LIMITATIONS.md#left-out-of-beta-1).

## 17. View lyrics
1. Play a track and on the bar use ⋯ → **View lyrics (가사 보기)**.
2. The first time, choose **Agree and search (동의하고 찾기)** (only the title · artist · album · length are sent), or **Do not send (보내지 않음)** and attach an LRC · TXT file.
3. Adjust timing with the clock button, then + / −, text size in `sidebar › Lyrics (가사) tab › Display (표시)`, find other editions with **Other edition (다른 판)** in the source line, and pick one in **Lyrics edition (가사 판)** when there are two or more.

**How to tell it worked**: The lyrics appear in the lyrics panel. More: Manual [§2.3](MANUAL.md#23-lyrics).

## 18. View and export listening history
1. In `Listening History (청취 기록)`, choose the **Recent (최근)** period and the **Source (출처)**.
2. **Export (내보내기)** → **JSON · includes counting criteria (JSON · 집계 기준 포함)** or **CSV · 1 row = 1 play (CSV · 1행 = 재생 1회)**.
3. To stop recording, turn off **Recording settings and counting criteria (기록 설정과 집계 기준) › Save listening history on this Mac (이 Mac에 청취 기록 저장)**.

**How to tell it worked**: The plays of the period · source you chose appear in the graph and the per-track history. More: Manual [§5](MANUAL.md#5-listening-history-page).

## 19. Turn off what goes out to the internet
1. In `Settings (설정) › Privacy (개인정보) › Network destinations (네트워크 목적지)`, turn off each destination.
2. To turn off only lyrics, the lrclib.net switch in `sidebar › Lyrics (가사) tab › Lyrics source (가사 출처)`.

**How to tell it worked**: Even with everything off, receiving sound · DSP · DSD conversion · DAC output · local playback work. More: Manual [§8](MANUAL.md#8-settings-window).

## 20. Send a support file when something goes wrong
1. **Help → Create diagnostics for a problem report… (도움말 → 문제 제보용 진단 만들기…)**. If you agreed to the optional diagnostic record at first launch, it is already recording: make the bundle right after the problem, before quitting the app. If it is off, press **Start diagnostic recording (진단 기록 시작)** and make the bundle the next time the problem happens.
2. **Create bundle and view contents (번들 만들고 내용 보기)** and check the contents (they include times, services, rates and random per-track labels; song names are masked).
3. Press **Send by mail (메일로 보내기)**; when the mail app opens, attach the .zip file from your Downloads folder (do not paste the contents: they get cut off). If you use another mail service (Gmail and so on), **Copy mail form (메일 양식 복사)** copies the address, subject and form to paste. Send the diagnostic bundle by mail only — do not put it on a GitHub issue.
4. At the moment something goes wrong, press **⌥⌃⌘K** (**Help → Mark That Something Was Off (방금 이상했음 표시)**); that time is marked in the diagnostic record so it is easy to find in the bundle.

**How to tell it worked**: **Show .zip file (.zip 파일 보기)** shows the .zip file in Downloads; opened, its folder has `support.json` · `manifest.json` · `tracks.json` · `README.txt`. More: Manual [§10](MANUAL.md#10-sending-a-support-file).

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
2. "Up to date (최신입니다)" means you are done. If there is a new version, the update window opens with what changed, and the new version is downloaded only when you choose to install it. The downloaded version is installed, and Fidenne restarted, only after its signature checks out. If there is no public release yet, it says so. When downloading, github.com may point to a different address (`release-assets.githubusercontent.com`); the update tool follows that pointer itself.
3. You do not have to press it: if you left the GitHub connection on at first run, the app checks every 4 hours by itself (and at launch and on wake), and when there is a new version the notice also shows a few lines of what changed. If the app is in the background, a notification banner appears once per version and clicking it opens the update window (the app asks for notification permission the first time; if you decline, you are told in the app window). To stop it, turn off **Check for a new version automatically, every 4 hours (새 버전을 자동으로 확인(4 시간마다))** at the bottom of `Settings (설정) › Privacy (개인정보) › Network destinations (네트워크 목적지)`.

**How to tell it worked**: "Current version (지금 판)" in the result window matches the version on the top row of the Settings window. More: Manual [§8](MANUAL.md#8-settings-window).

## 24. Volume notice before sound starts · turning output monitoring on and off
1. In **Start with the volume lowered (음량을 낮추고 시작하세요)**, which appears at the first play, lower the DAC · amp volume and press **Lowered it, start (낮췄어요, 시작)**. Raise the volume slowly.
2. To stop the notice every time, turn off `Settings (설정) › Sound safety (소리 안전) › Volume notice every time it turns on (켤 때마다 음량 안내)` (a DAC you use for the first time still shows it once).
3. Keep `Settings (설정) › Sound safety (소리 안전) › Mute when a signal not in the music appears (음악에 없는 신호가 나오면 음소거)` on.

**How to tell it worked**: Playback starts and there is no mute row at the head of the window. More: Manual [§1](MANUAL.md#1-first-launch--the-five-step-first-run-setup) · [§8](MANUAL.md#8-settings-window).

## 25. See and control YouTube Music (Chrome) from Fidenne
1. Turn on **YouTube Music (experimental)** in `Settings › General` first, then turn on `Settings (설정) › Privacy (개인정보) › YouTube Music › Connect with Chrome · Edge extension (브라우저 확장과 연결 (Safari · Chrome · Edge))`, and in **Setup guide… (설치 안내…)** choose **Chrome** or **Edge**.
2. Follow the guide window — **Copy address (주소 복사)** → paste it in the address bar and press Return → turn on **Developer mode (개발자 모드)** → **Load unpacked (압축해제된 확장 프로그램을 로드합니다)** → **Copy path (경로 복사)** → in the file window ⌘⇧G · ⌘V · Return · **Open (열기)**.
3. Reload the YouTube Music tab that was already open with ⌘R and play a track.
4. A browser that puts unused tabs to sleep leaves YouTube Music unable to answer — add `music.youtube.com` as an exception: Chrome under Settings → Performance → Memory Saver → **Always keep these sites active**, Edge under Settings → System and performance → Resource saving → **Never put these sites to sleep**.

**How to tell it worked**: The line under the guide window says `1 browser connected (브라우저 1개 연결됨)` and the bar shows that track and "YouTube Music (browser) (YouTube Music (브라우저))". After updating the app, press ↻ once on the **Fidenne for YouTube Music** card in `chrome://extensions` (Edge `edge://extensions`) and reload the tab with ⌘R. More: Manual [§8.1](MANUAL.md#81-using-youtube-music-chrome-extension).

## 26. Play YouTube Music tracks from the Streaming page
1. Press the service button before the Streaming page's search field and choose **YouTube Music**. If it says "Not connected (연결 안 됨)", do section 25.
2. In **My playlists (내 재생목록)**, open a list and press **Play all (전체 재생)** (or one track). If there is no list, open that screen once in YouTube Music — within a few seconds it appears as `From browser (브라우저에서)`.
3. To search, type in **Search in YouTube Music (YouTube Music 에서 검색)** and press Return.

**How to tell it worked**: The status row says `Playing in Chrome (Chrome 에서 재생 중)` and the track and the previous · play · next buttons appear. More: Manual [§8.1](MANUAL.md#81-using-youtube-music-chrome-extension) · [§3](MANUAL.md#3-streaming-page).

## 27. Search once, add a track that is not in your library to the Apple Music library, and play it
1. On the Streaming page, set the service to **Apple Music**, type in the search field and press Return. Results run **Apple Music** (my library) → **Apple Music catalog (Apple Music 카탈로그)** → **Local library (로컬 보관함)**.
2. On a catalog row press **Add to library (보관함에 추가)** and, in the confirmation the first time, **Add (추가)**.
3. The row changes to `Added · appearing in the library (추가했습니다 · 보관함에 나타나는 중)`, then its button becomes **Play (재생)** — press it. Spotify results are under the **Spotify** tab at the top.

**How to tell it worked**: The added track also shows in the Music app's library. More: Manual [§3](MANUAL.md#3-streaming-page).

## 28. Continue a track started in the Music app in Fidenne's queue
1. Start a track in the Music app. Press the cover on Fidenne's bottom playback capsule to open the large playback view; the following tracks appear in **Up next (다음 재생)**.
2. To let Fidenne decide the order, use ⋯ on a track row → **Play next (다음에 재생)** · **Add to end of queue (대기열 끝에 추가)**, or the bar's shuffle · repeat.
3. If three buttons appear, choose **Continue this album (이 앨범 이어 듣기)** · **Return to Fidenne's list (Fidenne 목록으로 돌아가기)** · **Leave it to Apple Music autoplay (Apple Music 자동 재생에 맡기기)**.

**How to tell it worked**: When a track ends, the next one in Up next follows. More: Manual [§2.2](MANUAL.md#22-bottom-playback-bar).

## 29. Connect Spotify for the first time (your own key)
1. In the connection window (press the dot beside Spotify on the Streaming page, or **Connect (연결하기)** on the Spotify screen), press **Open developer dashboard (개발자 대시보드 열기)** and create an app in the Spotify developer dashboard.
2. Put the address shown in the field into that app's Redirect URI (the **Copy (복사)** button beside it copies it).
3. Paste the dashboard's **Client ID** into Fidenne's field (do not enter the Client Secret).
4. Press **Check key (키 확인)**, then **Connect Spotify (Spotify 연결)** and allow it in the login window.

**How to tell it worked**: Searching with Spotify in the Streaming page's service list returns results, and the connection window has **Refresh playback permission (재생 권한 갱신)** · **Disconnect (연결 해제)**. Without a key, sound processing of tracks played in the Spotify app still works. More: Manual [§3](MANUAL.md#3-streaming-page).

## 30. Get the beta and report a problem
1. Get the signed and notarized `.dmg` from the releases page (`https://github.com/fidenne/fidenne/releases`) (Apple silicon Mac, macOS 15 or later).
2. Make a support file as in section 20 and send it to **fidenne.support@gmail.com** (**Send by mail (메일로 보내기)** or **Copy mail form (메일 양식 복사)** fills in the address, subject and form).
3. Write the DAC and output mode · what you were doing and what you heard or saw. The app version and macOS version are already in the form and the bundle. Send security problems by mail instead of a public issue.

**How to tell it worked**: The mail has the above and the support file. The app sends nothing on its own. More: Manual [Beta notice and where to report](MANUAL.md#beta-notice-and-where-to-report).

## 31. Use YouTube Music in Safari
1. Turn on **YouTube Music (experimental)** in `Settings › General`. Safari is independent of the Chrome · Edge connection switch.
2. Quit Fidenne and make sure it is in the **Applications (응용 프로그램)** folder. Opened from the Downloads folder or from inside the .dmg, Safari does not show the extension and Settings shows `Safari 확장은 Fidenne을 응용 프로그램 폴더로 옮긴 뒤 다시 열어야 Safari에 보입니다.` (move Fidenne to the Applications folder and open it again). After moving it, open it from there.
3. Press **Open Safari Settings (Safari 설정 열기)** in `Settings › Privacy › YouTube Music`. If Safari's extension settings open, turn on Fidenne's YouTube Music extension; if only Safari opens, turn it on in Safari › Settings › **Extensions (확장 프로그램)**.
4. On the music.youtube.com tab press the Fidenne icon in the row of extension icons next to Safari's address bar, and allow it to read `music.youtube.com` once (**Always Allow**).
5. Open music.youtube.com and play a track. If the tab was already open, reload it with ⌘R.

**How to tell it worked**: The bottom bar shows that track. Safari 18.4 or later is required. If the bar stops, reload that tab once. If it does not work, see the [Troubleshooting guide](TROUBLESHOOTING.md). More: Manual [Using Safari](MANUAL.md#using-safari).

## 32. Save an album to your library
1. In the Streaming page pick a service and open an album.
2. Press the **라이브러리** (Library) button in the album header (it may read **YouTube Music에 저장**, save to YouTube Music).
3. Spotify saves at once and the button becomes **저장됨** (Saved). If a notice about the save permission appears, connect **Spotify 연결** again in the Spotify connection window (the dot beside Spotify on the Streaming page).
4. For Apple Music you see `보관함에 넣었습니다. Music 앱에 보이기까지 조금 걸릴 수 있습니다.` (added; it can take a while to show in Music), and a moment later the button becomes **저장됨**. If it is slow, refresh the Music app.
5. For YouTube Music, that album's page must be open in the browser. Pressing the button makes the extension press the page's save control once and report the result.

**How to tell it worked**: The button becomes **저장됨**, or you see `이미 저장되어 있어요.` (already saved) · `YouTube Music 페이지에서 저장을 확인했어요.` (confirmed on the YouTube Streaming page). It also shows in the service's own library (Apple Music may be slow). More: Manual [§3](MANUAL.md#3-streaming-page).

## 33. Reorder songs your way
1. Open a playlist or album.
2. Press **순서 조정** (Reorder) in the play row (it is available for two or more songs once the list has been read in full).
3. Drag song rows to move them. With the keyboard select a row and use ⌥↑ · ⌥↓; if dragging is hard, use the row's **위로 옮기기** (move up) · **아래로 옮기기** (move down). ⌘Z undoes a wrong move.
4. Press **완료** (Done).

**How to tell it worked**: The **#** column shows your own order and playback follows it. The playlist's order at the service is unchanged. Home sections and playlist tiles can be dragged too. More: Manual [§3](MANUAL.md#3-streaming-page).

## 34. Translate lyrics with AI
1. Get your own API key on the site of a provider (Anthropic Claude · OpenAI · Google Gemini). Charges go to your account.
2. In the collapsed **AI provider settings** under `sidebar › Lyrics tab › Translation steps (번역 단계)` pick the **Provider (제공자)** and **Model (모델)**, paste the key into the **API key (API 키)** field and press **키 저장** (save key).
3. Press **AI 가사 번역 켜기** (turn on). A window says what goes where; read it and press **켜기**.
4. In the lyrics column turn on **Korean translation (한국어 번역)**. If you want, limit the count with **하루 요청 상한 사용** (daily limit).
5. To do it with no key, use **Translate on this Mac (Apple Intelligence) (Mac 안에서 번역 (Apple Intelligence))** in the provider list. It needs macOS 26 or later, an Apple silicon Mac and Apple Intelligence turned on, and the lyrics never leave the Mac.

**How to tell it worked**: A translated line appears under each original line. To delete, use **이 번역 지우기** (delete this translation) under the lyrics, or **AI 번역 전부 지우기…** (delete all) for everything. If it does not work, see the AI lyrics translation line in the [Troubleshooting guide](TROUBLESHOOTING.md). More: Manual [§8](MANUAL.md#8-settings-window).

## 35. Change the loudness with the DAC volume slider
1. Drag the **DAC volume (DAC 음량)** slider under the ⋯ and Up next buttons in the bottom bar (keep it low before playback starts).
2. If the slider is dimmed, hover to read why. During DSD · integer output, or with a DAC that has no volume control, use the DAC's own knob.

**How to tell it worked**: The slider follows the value read from the device and the loudness changes. More: [Troubleshooting guide](TROUBLESHOOTING.md#dac-volume-and-dsd-dop--integer-pcm).

## 36. When Fidenne stops while opening
1. If two starts in a row do not finish, a **시작 복구** (Startup recovery) window appears on the third start. No setting is erased.
2. **안전하게 시작** (start safely) enters for this one run with the engine · capture · browser extension · auto-play connections off.
3. To report the problem, build the material with **진단 만들기…** (make diagnostics) and send it (section 20).
4. Quit and open the app again to return to normal. If nothing looks wrong you can also press **그대로 시작** (start as usual).

**How to tell it worked**: The window shows `안전 시작 중` (safe start) and you can open Settings. More: Manual [When startup fails twice in a row](MANUAL.md#1-first-launch--the-five-step-first-run-setup).

## 37. Choose the PCM output rate · follow the source's rate family
**What you need**: output mode **PCM oversampling** (local files in PCM Direct keep the source rate, bypass processing and disable dither).
1. In `I/O · Diagnostics (입출력 · 진단) › Output method (출력 방식)` choose **PCM oversampling (PCM 오버샘플)** and open `Advanced (고급) › PCM`.
2. In the **Output rate (출력 레이트)** popup choose a rate (44.1 · 48 · 88.2 · 96 · 176.4 · 192 · 352.8 · 384 · 705.6 · 768 kHz). A rate the device does not take is greyed with `This device doesn’t accept it`. If the chosen rate is not taken, the **Change to ○○ kHz** button that appears goes to the highest rate the device takes.
3. Optional: to match the song's family, turn on **Follow the source's rate family (음원 계열 따라가기)**. A 44.1 kHz-family song goes out in the 44.1 family and a 48 kHz-family song in the 48 family, and the popup becomes multiplier rows such as `88.2 / 96 kHz (×2)`.
4. Optional: to use the highest multiple the device takes instead, choose the first row of the popup, **Auto (highest the device takes) (자동(장치 최고))**.

**How to tell it worked**: the line under the popup says what actually happened, such as `Source 44.1 kHz → output 176.4 kHz (×4) · 24-bit`, and with Auto it shows `Auto → 384 kHz`. It goes briefly quiet between songs that change family. More: Manual [§7.1](MANUAL.md#71-independent-output-control--output-mode).

**If it does not work**: when the DAC does not take the family, a notice says it converted to the other family. A song whose rate is not known yet shows `Source rate not confirmed yet — keeping the current family`.

## 38. Choose how songs join · when the DAC cuts the first sound
**What you need**: a local file played as **PCM oversampling** (for streaming sound that Fidenne receives and processes, and for DSD, these choices do not apply).
1. In `I/O · Diagnostics › Advanced › PCM`, under **Between songs (곡 사이)** choose **Unchanged (그대로)** (leaves the music untouched and joins songs with digital silence) or **Smooth (부드럽게)** (fades the last 0.02 s). It applies from the next song.
2. If the first sound is cut off while the DAC locks to the new rate when songs change, make **Wait when the rate changes (레이트를 바꿀 때 기다림)** longer: **0.5 s** · **1 s** · **2 s**. It is set per DAC; the default is **0.25 s** (**Off** is also available).

**How to tell it worked**: each song shows a line such as `This song: Unchanged · the rate changed, so 250 ms of silence comes first` or `This song: Unchanged · the rate stays the same, so no silence comes first`. More: Manual [§7.1](MANUAL.md#71-independent-output-control--output-mode).

**If it does not work**: the wait cannot be set before an output device is chosen (`Choose an output device to set this.`). Fidenne processes the sound and sends it to built-in speakers and AirPods too, but macOS sets the device rate, so Fidenne does not change it and this wait setting does not apply.

## 39. Process built-in speakers · AirPods · HDMI with Fidenne
1. In the output DAC picker choose a device such as the built-in speakers, the headphone jack, AirPods (Bluetooth) or an HDMI monitor. It does not get `· PCM Direct only`.
2. Choose **PCM** as the output method and start playback. The first time, `Turn the Mac volume down to 0 or very low before starting, then raise it slowly while you listen.` appears; lower the Mac volume and press the start button.
3. Turn on EQ · Ostrum · Crossfeed, choose a filter and listen.

**How to tell it worked**: Fidenne processes the sound and sends it; macOS mixes the result through its system mixer before sending it to the device, so it is not bit-perfect. The output line shows `via system mixer · not bit-perfect`, and the bit depth and dither rows are greyed. More: Manual [§7.1](MANUAL.md#71-independent-output-control--output-mode).

**If it does not work**: if an app using the AirPods microphone is open, the sound drops to call quality and Fidenne pauses its processing; close that app and it restarts by itself. If playback stops because another app changed the device rate, click Play again. For a bit-perfect output use an external DAC.

## 40. Put an Audio Unit plug-in in the path
1. On the sidebar **DSP › Plug-in (플러그인)** page press **Add Plug-in (플러그인 추가)** and choose an effect plug-in from the list. A plug-in seen for the first time is checked before it can be used.
2. Press **Turn On (켜기)** on its card. There are at most 4 slots.
3. Optional: **Open Editor (편집기 열기)** opens the plug-in's screen to adjust values, and dragging ≡ (or ⌥↑ · ⌥↓) reorders them.

**How to tell it worked**: from the next playback the card shows `Working · Delay ○ ms`. More: Manual [§6.9](MANUAL.md#69-plug-in-page).

**If it does not work**: read the reason on the card (cannot be used as stereo · does not accept the sample rate · cannot keep up …) and press **Turn Back On** or **Reload**. To take it out, press **Remove**.

## 41. Import an EQ file (REW · Equalizer APO · AutoEq)
**What you need**: a filter-settings text file (.txt, up to 2 MB).
1. In the EQ panel of Playback Chain press **Import…** under **My EQ**, and choose the file, or drop the file on the EQ settings area.
2. Read **Imported** and **Not imported**.
3. Check the name and press **Save to My EQ**.
4. Choose the EQ you just saved in **My EQ** to apply it.

**How to tell it worked**: `Saved as “name” — choose it in My EQ to apply it.` appears. Saving alone does not change the sound.

**If it does not work**: `No Preamp or Filter lines found …` means it is not REW · Equalizer APO · AutoEq filter text; if a line cannot be read, the line number is given and the whole file is not imported. A GraphicEQ curve is opened with **Open EQ preset… (EQ 프리셋 열기…)** on the DSP page.

## 42. Add songs to a playlist, group them and remove them from history on Home
1. On the streaming page's home screen, drag a song tile from **Played today (오늘 들은 것)** onto a playlist tile in **My playlists**. To avoid dragging, use the tile's ⋯ → **Add to Playlist ▸**.
2. Optional: to group songs of the same day, use the tile's ⋯ → **Group with Another Group of This Day ▸**.
3. Optional: to hide an entry you do not want to see, press the tile's ⋯ → **Remove from History** (or select the tile and press ⌫).

**How to tell it worked**: a toast such as `Added to ‘Name’` or `Removed from history` appears. To take it back press **Undo** or ⌘Z within 10 s. What is written to a service playlist has no undo button.

**If it does not work**: a no-drop cursor means the place does not take it (a line gives the reason). A Spotify list needs **Allow…** once, and an Apple Music list needs the Music app to be open. Removing from Home does not remove it from the listening-history statistics.

## 43. Call play and bypass of sound processing from Shortcuts
1. In the Shortcuts app, make a new shortcut and choose an action of **Fidenne**: **Play / Pause** · **Next Song** · **Previous Song** · **Song playing now** · **Bypass sound processing** · **Choose EQ Preset**.
2. Set on / off for **Bypass sound processing**, and choose a saved EQ name for **Choose EQ Preset**.
3. Run the shortcut. In Siri · Spotlight say it like `Play or pause in Fidenne` (English phrases).

**How to tell it worked**: Fidenne does the action (playback goes the same way as the window's buttons). **Bypass off** restores only what the on step turned off. More: Manual [§2.4](MANUAL.md#24-menu-bar-icon--menus).

**If it does not work**: controlling Apple Music · Spotify needs the automation permission in System Settings, and YouTube Music needs a connected tab. The output device, volume and output method cannot be changed from Shortcuts.

## 44. Turn on the lyrics pronunciation line and reorder the lines
1. In the sidebar **Lyrics (가사)** tab, under **Display (표시) › Line order · Visibility (줄 순서 · 보이기)**, turn on the eye of the **Pronunciation** line (off by default).
2. Optional: drag the lines (or press ⌥⌘↑ · ⌥⌘↓) to reorder original · pronunciation · translation, and use the eyes to show or hide each. At least one must stay shown.
3. Optional: if a pronunciation is wrong, click the line in the Lyrics tab, edit it and press Return (Esc cancels).

**How to tell it worked**: the lyrics panel and the album screen show the pronunciation line in your order with `Pronunciation lines are estimates`. A line you edited is marked `Pronunciation I edited`. The reading is macOS's estimate and can be wrong.

## 45. Sleep timer and volume keys
1. In the Playback menu (the menu bar menu has it too) choose a length such as **30 min** under **Sleep Timer (취침 타이머)**, or **When This Song Ends**, or **Custom…** (1 to 720 minutes).
2. To end it, choose **Turn Off Timer**.
3. Change the volume with **Volume Up** (⌘↑) · **Volume Down** (⌘↓) · **Mute** (⌥⌘↓) in the Playback menu.

**How to tell it worked**: the menu title reads `Sleep Timer · ○ min left`, and when it ends playback pauses. Quitting the app also removes the timer.

## 46. Use the screens in English or Japanese
1. Put English or Japanese ahead of Korean in macOS's language order (System Settings › General › Language & Region).
2. Restart Fidenne.

**How to tell it worked**: the sidebar and Settings appear in English or Japanese. The app has no language switch of its own, and if none of the three is first it is Korean. The translations are AI drafts and a native speaker has not reviewed them, so some sentences may be awkward.
