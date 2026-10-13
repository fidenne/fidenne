<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/MANUAL.md at commit 5fe772e9baf1fbd1be25fefcf85283d74d6a03f9 -->

# Fidenne User Manual

## One-page summary

**What Fidenne is** — a macOS app that takes the sound of Apple Music, Spotify and YouTube Music, or the music files on this Mac, shapes it with EQ, Ostrum, crossfeed and a filter, and sends it to a **wired USB external DAC** (required). It needs an Apple silicon Mac and **macOS 26 or later**.

**The five pages** (sidebar, ⌘1–⌘5)

- **Music (음악)** — pick a service, search and play, and resume from the home screen. ([§3](#3-music-page))
- **Library (보관함)** — index the music folders on this Mac and manage playlists and the queue. ([§4](#4-library-page))
- **Listening History (청취 기록)** — view what you listened to by period and source, and export it. ([§5](#5-listening-history-page))
- **DSP** — Response graph, Equalizer (with Auto EQ), Ostrum, Crossfeed, A/B comparison. ([§6](#6-dsp-page))
- **I/O · Diagnostics (입출력 · 진단)** — output mode, input and output devices (DAC), filter · modulator, and the path the sound takes now. ([§7](#7-io--diagnostics-page))

**The three output modes** (`I/O · Diagnostics (입출력 · 진단) › Output mode (출력 방식)`, [§7.1](#71-independent-output-control--output-mode))

- **PCM Direct** — Fidenne does not process the sound. It goes playback app → macOS → DAC as is; if the rates differ, macOS converts.
- **DSD (DoP)** — the engine processes the sound and sends it to the DAC as DoP.
- **PCM 352.8 kHz** — the engine processes the sound and sends 352.8 kHz integer PCM (24 · 16-bit, dither selectable).
- With EQ · Ostrum · Crossfeed off, DSD and PCM 352.8 kHz apply no tone-changing processing, but the conversions that format needs (upsampling filter · DSD modulator · dither · headroom) still run.

**Where to get help** — "how do I do X" is in the [task-by-task instructions](HOW-TO.md), when something fails in the [Troubleshooting Guide](TROUBLESHOOTING.md), and the reasons in the [Explanations](EXPLANATIONS.md). To report a problem, see [§10](#10-sending-a-support-file).

- Scope: the Fidenne 0.4.29 source tree (the build number is the commit count — §0). It describes **only what the app has now** — every item was checked against the on-screen strings and the code one by one,
  and features that exist only in a plan are left out. The app's screen text is currently Korean only, so on-screen names are given in English with the Korean original in parentheses.
- Markers: **[Experimental]** (〔실험〕) marks an option the app itself labels "experimental" (실험); **[Dev build]** (〔개발 빌드〕) marks something that exists only in the personal (PERSONAL) build
  and not in the released build.
- This document is a **reference** — what each page has and what it does, in the same order as the app's contents. For where to look when something goes wrong, see the
  [Troubleshooting Guide](TROUBLESHOOTING.md).
- To look things up by "what I want to do", see the [task-by-task instructions](HOW-TO.md).
- For why the app behaves the way it does, and **how it used to behave**, see the [Explanations](EXPLANATIONS.md).

## 0. At a glance

The summary is in the [one-page summary](#one-page-summary) at the top. The figure below shows the path the sound takes — **PCM Direct**, which does not use the engine, is the last line.

```
Playback app ──(capture: Fidenne Inlet or Process Tap)──┐
                                                    ├─▶ Fidenne engine ─▶ DSD (DoP) or PCM 352.8 kHz ─▶ DAC
Music files on this Mac (Library page) ─────────────┘
Playback app ─▶ macOS PCM ─▶ DAC                    (PCM Direct — no engine)
```

The window's **sidebar** (the page list) runs the full height of the window and is separated from the main area by a single line. Order: Music (음악) · Library (보관함) · Listening History (청취 기록) · DSP · I/O · Diagnostics (입출력 · 진단) (+ [Dev build] Development · Diagnostics (개발 · 진단)). The gear-shaped **Settings… (설정…)** row at the very bottom opens the Settings window (§8). The **GitHub** row below it opens Fidenne's public repository page in the browser (only in builds that have a public repository written in them).
The sidebar button (an icon of a box with a vertical bar) stays in the **same place** whether the sidebar is collapsed or expanded — in a window, right after the traffic-light buttons; in full screen, at the very start of the page title bar. When the sidebar is collapsed, the page title moves aside to sit next to the button. In the large playback view, the same place becomes the close (×) button.
The shortcuts ⌘1… follow this order. The window reopens with the **size and position where you last left it** and the **page you last viewed** (on the first launch, Music — the
macOS app convention). Only when you change **Interface scale (인터페이스 배율)** in Settings › General (일반) does the app resize the window to fit that scale. The sidebar header shows `Fidenne`, and on the line under it the version and build number (`0.4.29 (commit count) · 개발자용` (for developers) or `· 배포판` (released build)).
The build number is that build's commit count. So it rises by itself with each commit, and the same commit gives the same number on any Mac that builds it. A bigger jump than before (37 → thousands) is normal.
When a line is narrow, the text gets slightly smaller and is not cut off.

### What Fidenne uses

Fidenne is a free app made by an individual and is not affiliated with Apple, Spotify or Google. Apple Music is a trademark of
Apple Inc., Spotify of Spotify AB and YouTube Music of Google LLC.

- **Apple Music** — Fidenne drives the Music app with AppleScript. It reads the library list with MusicKit; for an Apple Music track you are
  playing it asks the Apple Music catalogue for the other spelling and the same song on other services and uses the answer in memory only
  (never kept). To follow each track's source rate it reads the Music app's audio log lines (not kept).
- **Spotify** — Fidenne drives the Spotify app with AppleScript. Search and playlist screens use only a Spotify developer key you create
  yourself (optional).
- **YouTube Music** — a browser extension reads the track on the open page and passes on controls such as play and pause. It never browses
  the site on its own: one press by you opens that one page. It never touches ads. Experimental.
- **Lyrics** — LRCLIB (lrclib.net). Lyrics belong to their rights holders.
- **Headphone measurements** — public measurement data from squig.link, fetched to this Mac and used for correction. The data belongs to each measurer; the app shows the measurer's name and a link to the original graph.
- **Song search and charts** — Apple's public search and charts. Their pictures are not kept on this Mac.
- **Sound** — taken from macOS audio (Core Audio) and processed only on this Mac. Never recorded or sent anywhere.
- **Kept on this Mac** — album covers and lyrics, temporarily, for quick display (removed 30 days after last seen).

The full list is in [Privacy](../../../PRIVACY.en.md).

## 1. First launch — the four-step first-run setup

On the first launch, a "Fidenne First-run Setup (Fidenne 처음 설정)" window appears. Move between steps with **Back / Next (뒤로 / 다음)**.

1. **The DAC the sound goes to (소리가 나갈 DAC)** — choose the output device. "Choose later (나중에 고르기)" is also allowed. If the device does not appear, plug in the DAC and refresh.
2. **How to bring the sound in (소리를 가져오는 방법)** — clicking anywhere in a box selects it.
   - **Fidenne Inlet** (recommended, selected from the start) — receives the playback app's original rate as is. If it is not installed, install it with **Install… (설치…)** right under it
     (macOS asks for the administrator password once, and restarts the audio service, so all sound cuts out briefly). If you press **Next** without installing,
     it receives through the System Tap — that one line is shown on the screen. You can also install it later on the I/O page.
     If something changes this device's rate during playback, the engine carries on at the new rate after 1–3 seconds of silence (it does not stop).
   - **System Tap (시스템 탭)** (Process Tap) — works immediately with no installation. It receives at 48 kHz. On the I/O page you can choose which app to receive from (§7.3).
   - Another loopback app is not a box to choose but a one-line note — if you already use one, choose that device on the I/O page under the input with
     **+ Another input device (+ 다른 입력 장치)**. The app neither ships another loopback app nor looks for one by name.
3. **Things macOS will ask (macOS가 물어볼 것들)** — permissions are not asked now; macOS asks the first time you use the feature. For each permission, "when / if you decline"
   is written (audio recording · system audio access; microphone (Fidenne Inlet · another input device); automation (controlling Music · Spotify); media library (Apple Music library)).
4. **Terms of use, internet connections and diagnostics (이용 약관과 인터넷 연결)** — the last step is a single screen. The full terms of use (seven items: free use · redistribution · modified copies · no warranty · limitation of liability · third-party components · no reverse engineering) come first, followed by four checkboxes: **Agree to all (전체 동의)** · **[Required] I agree to the terms of use (이용 약관에 동의합니다)** · **[Optional] Use internet features (인터넷 연결 기능 사용)** · **[Optional] Problem-report diagnostic records, stored only on this Mac (문제 제보용 진단 기록)**.
   The optional boxes start unticked. **The terms box is required** — the **Start (시작)** button stays disabled until it is ticked, and **Decline and quit (동의하지 않고 종료)** quits the app. If you leave the optional boxes off the app still opens and plays (only the features that use the internet are turned off). Diagnostic records are numbers and states only, with no personal data or audio, and you can change every choice later in Settings › Privacy.
   If you finished the first-run setup before this version, the same terms and an **Agree / Quit (동의 / 종료)** sheet appear once at the next launch, and appear again when the terms change.

**How to tell it worked**: when you finish the four steps, the sidebar and pages appear in the same window, and from the next launch the first-run setup does not appear again.

**When you play for the first time — the volume notice.** Each time you launch the app, when you press the first start (playback · turning on the engine · file playback · PCM Direct), a sheet reading
"Lower the volume and start (음량을 낮추고 시작하세요)" appears **before** any sound is made — turn the DAC/amp volume down to 0 or very low and press **I lowered it, start (낮췄어요, 시작)** (Return), then raise it slowly while listening.
**Cancel (취소)** (Esc) starts nothing. It also appears once, as "You are using ○○ for the first time (○○을 처음 씁니다)", when you start with a DAC that this app has not used before. The notice has no "Don't show again";
the place to turn it off is one place, Settings › **Sound safety (소리 안전)**, and even when it is off, a first-time DAC is asked about once. If the first-time DoP question (§7.2) applies at the same time, they appear one sheet at a time, in the order volume notice → DoP question.

**Output monitor**. The engine only keeps reading the signal immediately before the output, after all processing, and when a shape that cannot come from music appears — holding at the maximum magnitude of one polarity for
more than 50 ms · a large direct current (DC) · a large signal in the inaudible ultra-high range — it mutes the rest of that playback and says what it saw and when, in one line at the window's head: "Output muted — … (출력을 음소거했습니다 — …)".
Stopping and playing again brings the sound back. Ordinary sound (including very loudly mastered tracks and bass boosted heavily with EQ) is not changed
by a single bit. When playback starts, and when the output is interrupted briefly and comes back, the first 20 ms is ramped up from 0 to prevent a click.

Internet destinations are turned on and off one by one (Settings › Privacy (개인정보) › Network destinations (네트워크 목적지)). **Even with all of them off, capture · DSP · DSD conversion · DAC output, and
local playback keep working, and audio is never sent out under any circumstances.** When a new destination is added, the "The features that use the internet have increased (인터넷을 쓰는 기능이 늘었습니다)"
sheet appears once more.

## 2. Always visible — header · bottom playback bar · menus

### 2.1 Page header

- The page name and description, and the **Playback Chain** button. Pressing it shows, line by line in the order the sound travels — **Source → Capture → Conversion → Band → DSP → Filter →
  Output → Device (음원 → 캡처 → 변환 → 대역 → DSP → 필터 → 출력 → 장치)** — with the **values the engine is using now**.
  - The dot and one word at the window's head describe the whole path — **Running · Processed (실행 중 · 처리됨)** (the Fidenne engine upsampled and passed through the DSP that is on) · **Running · Not processed (실행 중 · 처리 없음)**
    (PCM Direct — Fidenne does not touch it, and macOS sends it to the DAC) · **Stopped (멈춤)** · **Preparing (준비 중)** · **Error (오류)** (a red exclamation mark). It never says "bit-perfect" —
    because even in PCM Direct, macOS sits in the middle and this is not measured.
  - **Source (음원)** line: the app producing the sound now. For Apple Music and Spotify, the name (and, when the engine is running, the original track's rate); for a YouTube Music tab with the browser extension connected,
    the browser the tab is running in, as in `YouTube Music (Edge)` (if two browsers are making sound, `(browser)`); if a browser is making sound without the extension,
    `Browser (Edge)` (`브라우저(Edge)`). YouTube.com videos are not seen by the extension, so they show as `Browser (…)`. When nothing is making sound, `No playing app (재생 중인 앱 없음)`.
  - **Capture (캡처)** line: the capture path (Fidenne Inlet · Process Tap · the name of a device chosen with +) · the rate the engine receives · the drop count. Before start, `· not started (시작 전)`; if there are drops, in red.
  - **Conversion (변환)** line: whether the original track's rate and the capture rate are the same — `None · 44.1 kHz as is (없음 · 44.1 kHz 그대로)`, and if they differ, in red `44.1 kHz → 48 kHz · the playback app or macOS changed it (재생 앱이나 macOS 가 바꿈)`.
    If the playback app does not report the original track's rate, `Unknown (모름)`. **Spotify does not report the original rate** — when the capture is at 44.1 kHz it only looks the same as Spotify's published stream spec, so the line says `Presumed none · 44.1 kHz (by spec — the playback app does not say) (없음으로 추정 · 44.1 kHz (규격 기준 — 재생 앱은 알려 주지 않음))` (hover for the reason). The measured value is the rate on the **Capture** line;
    the **Source (음원)** line carries only a rate the playback app reported (Apple Music track info and so on).
  - **Band (대역)** line: the band the engine saw in the incoming sound — `Full band · confidence 93% (풀대역 · 신뢰도 93%)`, and if there is almost no sound above some frequency, `Almost no sound above 16.0 kHz · confidence 88% (16.0 kHz 위로 소리가 거의 없음 · 신뢰도 88%)` — drawn in red only when that frequency is below 18 kHz; a cut at 18 kHz or above (common in lossless sources too, around 20 kHz) keeps the normal colour. The colour follows the displayed one-decimal value, so 17.96 kHz is shown as `18.0 kHz` in the normal colour.
    This line measures only **where the sound stops** — not why. Lossy compression (MP3 · AAC) looks like this, and so does the mastering-stage band limit that a lossless original carries
    (it can be a property of the original master, and near 20 kHz it usually has nothing to do with what you hear). **Confidence** is how steep and deep the stop is, not the probability that the source is lossy. If the sound is quiet or has only now started, `Not yet judged · … (판정 전 · …)`. The Conversion and Band lines are absent in PCM Direct (there is no capture).
  - The end of the **Device (장치)** line shows the underrun count (in red if there are any).
  - The **DSP** line is a set of chips — **EQ · Ostrum · Crossfeed**. Clicking a chip **turns it on or off on the spot** (a filled chip and a filled dot = on, an empty chip and an empty dot = off,
    `–` = no report from the engine). It is the same as the on/off on the DSP page — EQ is heard immediately and saving is the DSP page's Save, and Crossfeed, when turned off, returns to the last
    preset (Low · Medium) when turned on again. The chip's `›` or **⌥-click** goes to that setting. In PCM Direct, instead of chips, `Not passed through in PCM Direct (PCM Direct 에서는 거치지 않음)`.
  - A line with `›` at its end goes **wherever you click on the line** to that part — EQ · Ostrum · Crossfeed go to that tab on the DSP page (directly under the graph),
    Filter · Output go to that card on the I/O page (expanded if it was collapsed), and Capture · Device go to the **Input and Output Devices (입력과 출력 장치)** card on the I/O page. The Source · Conversion · Band lines
    show values only. The place you arrive at is marked briefly with an outline.
    Even if you leave the DSP page on another tab and come back, the tab of the line you clicked opens.
  - The output format line shows dither — for DSD, `· Experimental dither on (실험 디더 켬)` (when on), for PCM, something like `· Dither default (디더 기본)`.
  - If the output device is not in the list, the line turns red and a **Search again (다시 찾기)** button appears in its place; if the connection was lost, a **Reconnect (다시 연결)** button.
  - In PCM Direct, the engine is not used, so the EQ · Ostrum · Crossfeed lines say `Not passed through in PCM Direct` and the switches rest.
  - The engine's part names (the rate the playback app announced · PCM-A chain · DSD readback · limiter · stabilization · profile revision · applied path) are inside **Details · values the engine reported (자세히 · 엔진이 보고한 값)** (collapsed).
  "Open I/O · Diagnostics (입출력·진단 열기)" goes to the detailed page.
- While the output is being prepared, "Preparing audio output · you can cancel the start request with Stop. (오디오 출력 준비 중 · 정지로 시작 요청을 취소할 수 있습니다.)" appears.
- When an error occurs, a red line and a fault description appear here (Troubleshooting Guide §1).

### 2.2 Bottom playback bar

Order on the bar: the mark of the service now playing (Apple Music / Spotify) · **output mode menu** · playback controls (shuffle · previous · play/pause · next ·
repeat, playback position) · additional playback functions (⋯) · **engine button**.

- **Output mode menu**: PCM Direct · "DSD · previous setting (DSD · 이전 설정)" · **Sound preset (사운드 프리셋)** (a list of recommendation cards) · saved presets · "Sound settings… (사운드 설정…)". Choosing a newly saved preset restores its engine output: DSD, or the saved PCM depth at 352.8 kHz. From PCM Direct, it returns to that engine output. A saved row is checked when its contents and output match the current settings. PCM Direct is chosen separately and is never saved in a preset. Older presets without an output setting retain the current engine format and are checked only on the DSD path.
- **⋯ additional playback functions**: the track menu (§2.7 — Play Next · Add to End of Queue | Show Lyrics · Track Info · Show in Playback App), with "Output settings… (출력 설정…)" under it.
  - "Output settings…" and "Sound settings…" in the output mode menu open the **I/O · Diagnostics page**, which has the filter · DSD conversion · PCM headroom, and
    expand **Details (자세히)** of the **"Filter · Modulator · Output Gain (필터 · 모듈레이터 · 출력 게인)"** card (§7.4).
- **Engine button**: at the end of the bar, the **switch** next to the status dot turns the engine on/off (start · stop · cancel preparing), and the dot beside it is the status (running · preparing · error) — clicking the dot opens
  the output diagnostics. **The engine switch does not play a track, and the play button does not turn off the engine**:
  - When you turn the switch on, an app that is playing continues, now through the engine. For an app that is paused, it plays only **when `After the engine starts (엔진 시작 후)` is an app name such as Apple Music or Spotify**,
    and if it is **Auto-detect · do not autoplay (자동 감지 · 자동재생 안 함)**, it plays nothing — if you play in the browser as it is, the browser's sound goes through the engine (§7.3).
    With **YouTube Music (browser) (YouTube Music(브라우저))**, once the engine is on it sends ▶ to the YouTube Music tab already open in the browser (it opens no tab and launches no browser).
    The menu bar's **Start (시작)** and the shortcut **Start Engine (엔진 시작)** work the same way.
  - **Pause pauses only the playback app and leaves the engine on.** To turn off the engine, use the switch. When the engine is off, pressing **Play** turns on the engine and plays the track.
- Shuffle and repeat work only on **a list played in Fidenne** (for an external app's queue, do it in that app).
- **In an Apple Music · Spotify list managed by Fidenne, when you press previous · next several times in a row** (⌘→ repeated, and so on), the list moves with each press, but to the playback app **only the last track is sent after the presses stop**
  (the first press after a pause goes at once). If the playback app has loaded the track but is still stopped, it is told to play once more, and if it is still stopped, the reason is shown but **the list is left
  as it is** — the play button resumes it. When an external app or browser manages the queue, that service handles track skipping.
- **Two-finger scrolling always scrolls the page. Values change when you scroll while holding ⌘** (it does not steal the scroll the way macOS's default sliders do).
  A value always moves by **the smallest digit visible on the screen** (EQ gain · knob dB 0.1, Hz 1 …) and does not skip to a coarser step. Adding **⌥ · Shift** makes
  the same hand movement raise it ten times more slowly (1/10 of the usual speed).
  Put the pointer over the **playback position** · a slider · an EQ number field · an Ostrum knob and, **holding ⌘**, swipe **up** with two fingers on the trackpad to raise the value and
  swipe down to lower it (following the system's "Natural scrolling" setting; a mouse wheel works too). Pressing **⌥ (or Shift)** together with **⌘** makes it slow.
  ⌘ only has to be held when the swipe **starts** — releasing it midway still lets that swipe change the value to the end, and a swipe that started without ⌘ belongs to the page even if you press it midway.
  After you lift your hand, the value does not move further from inertia. Scrolling over a control without ⌘ moves the page, and over that control **"Scroll while holding ⌘ to adjust the value" (⌘ 누른 채 스크롤하면 값 조절)**
  appears briefly (the first three times whenever you have been away for more than 20 seconds, and after that at most once an hour).
  The old rule (without ⌘, the value changes when you move the pointer into the control and then scroll) is still used if you choose **When started over a control (조작 위에서 시작하면)** in **Settings → Controls and Shortcuts (조작과 단축키) → "Change values with two-finger scrolling (두 손가락 스크롤로
  값 바꾸기)"**. With **Off (끔)**, scrolling is always received by the page. If you had this setting turned on before, after the update it changes once to **Hold ⌘ (⌘ 누른 채)** and the window's head shows
  "The update changed two-finger scrolling, so it was reset to the recommended value (업데이트로 두 손가락 스크롤이 바뀌어 권장값으로 초기화했어요)" — **Go to the setting (설정하러 가기)** takes you to
  that line.
- **Trackpad haptics**: in **Settings › Controls and shortcuts (조작과 단축키)** choose **Off · Weak · Medium · Strong (끔 · 약 · 중 · 강)**; Medium is the default.
  Weak plays only at zero and the ends. Medium plays lightly on each step, limited to about 16 per second during fast movement. Strong plays on every changed step, including fast movement. Medium and Strong also mark zero and the ends.
  A step is the smallest displayed unit (EQ gain 0.1 dB, frequency 1 Hz, knob dB 0.1), including Shift · ⌥ fine adjustment. Feedback plays while you drag with a Force Touch trackpad or swipe while holding ⌘. Loading a preset, typing a number and using a mouse produce no feedback.
  Set the trackpad's own strength in **System Settings › Trackpad**. A previously enabled setting becomes Medium; a disabled setting stays Off.
- **The click target is the whole visible box**: the Equalizer · Ostrum · Crossfeed pickers, the `>` collapse line, list rows, and round buttons work wherever in the box you click, not
  only on the text.
  The playback position moves only the display by 1 second per step (0.1 second with ⌥), and then **once, when the swipe ends**, jumps to that place (for the wheel, after a 0.35-second pause).
  EQ gain · Preamp · Freq · Q are heard immediately, the same as when dragging (to keep them, Save on the DSP page ⌘S — §6.2). The PCM headroom slider is applied
  immediately, the same as when dragging, and becomes manual.
- When a browser (a video site, etc.) or another app is making sound and Apple Music · Spotify is paused, the bar writes **`System sound — source unknown (시스템 소리 — 출처를 모름)`**.
  In the meantime, the paused track is not treated as the current track — it is not counted in Listening History, lyrics are not searched, and it is not posted to macOS's "Now Playing" either. When you play
  the playback app again, it goes back to that track. Sounds from apps not on the app list (notification sounds, etc.) are not considered.
- When Spotify is played on another device (a PC, a phone), the Mac's Spotify app also shows that song, but once a few seconds pass with no Spotify sound coming from this Mac,
  the bar writes only one line, **`Spotify — playing on another device (Spotify — 다른 기기에서 재생 중)`**. That song is not counted in Listening History, its lyrics and queue are not searched, and it is not posted to macOS's
  "Now Playing" either. Control it in Spotify on that device. When you play Spotify on this Mac again, it goes back to that track at once.
- Clicking the album cover opens the **large playback view**. It has three columns — the first holds the album cover and playback controls, the second (middle) the **Up Next list (다음 재생 목록)** (Now Playing · upcoming tracks) and
  **Lyrics**, and the third the **Playback Chain** (the same content as the one in the window header). The wider the window, the wider the cover column.
  To close — the close button (×), clicking the cover again, or **Esc**.
  - **Lyrics controls**: in a narrow column, the lyrics-control row, **Lyrics · Playlist (가사 · 재생목록)** switch and hint are arranged on separate rows. The attach-lyrics-file · search-again · Korean-translation buttons and **Lyrics edition (가사 판)** menu are neither hidden nor made smaller.
  - **Collapsing and expanding the Playback Chain column**: press or drag the handle (`›`) in the middle of the column's inner edge, or press **⌥⌘P**. While dragging, you feel one tap as you pass the halfway point, and on release it goes to the nearer side. Collapsed, the column's width is 0 and only the handle
    remains (with a dot on it if there is something to check). Collapsing keeps the ratio of the cover and lyrics columns. In a narrow window it starts collapsed.
  - **Service label**: between the two times under the playback bar, the service icon and name (`Apple Music ↗` · `Spotify ↗`). Pressing it opens the current track in that service —
    Spotify goes straight to the track's address; Apple Music looks the track up in the store by track name and artist (asking Apple once when you press) and opens that track's page,
    and if it cannot find it, opens only the playback app. The service icon on the playback bar below does the same.
  - **Search**: **⌘F** or the magnifier (`검색`, "Search") in the tool row under the middle column. A search panel opens over the album view — choose **Music Explore (음악 탐색)** (searching a service) or **Library (보관함)**
    (your files), and choosing an item plays it · adds it to the queue as on each page. When a new track starts, the panel closes and the album view changes to that track.
    **Esc** or `닫기` ("Close") returns to the album view as it was.
  - The background does not blur or cover the cover art; it is a pale gradient of one or two colours taken from the cover (the window colour as is when the cover has almost no colour).
  - Even if you have not played a list in Fidenne, if you are listening with **Spotify**, **`Up next · Spotify queue (이어지는 곡 · Spotify 대기열)`** appears in the upcoming-track place (when Spotify is
    connected — Spotify is asked once each time the track changes, and this is not a new internet destination). It is a view-only list, so clicking a row does not play it.
    **Apple Music does not tell other apps its next-track list**, so the upcoming tracks are empty and say so — if you play a list in Fidenne, it is shown.
  - When you play a Spotify list in Fidenne, **the next tracks (up to 99) are sent to Spotify together.** So when you control this Mac's Spotify from the Spotify app on a phone
    (Spotify Connect), "Next" and "Previous" follow the list, and Fidenne's upcoming tracks move along with it.
- When space is tight, the bar becomes two rows — when the window is narrow, or when the sidebar or the Up Next list is open and there is not enough room for the track title, the track and the playback buttons
  move to the lower row. This is so the title is not cut down to a character or two.
- The bar (the playback capsule) floats on **every page** — so you can touch A/B and the like immediately on any page. The end of a page
  extends down by the height of the capsule, so if you scroll to the last line it rises above the capsule. If content passing behind the capsule during scrolling
  interferes with the text, change the material · transparency in **Settings › General's "Playback capsule (재생 캡슐)"** (§8).

### 2.3 Lyrics

- When you play a track, the lyrics appear in the lyrics panel. Internet lyrics (lrclib.net) need **consent the first time** — "Agree and search / Do not send (동의하고 찾기 /
  보내지 않음)". What is sent is **only the track title · artist · album · length**; audio and account information are not sent.
- **Link a lyrics file**: link an LRC or TXT file to this track (it can be unlinked).
- **Lyrics timing**: if the lyrics come before the music, +; if they are late, −. It applies only to this track and is remembered. "Reset (초기화)".
- **Link text (글자 연결)**: fit the text of a lyrics file that has no timing to the timing of the current lyrics (for example, automatic captions). For this track only.
- **Korean translation**: when on, a small Korean line appears under the original line. If there is a timed Korean edition of the same track's lyrics, that edition is attached in time, and if there is none or too few lines match, the whole track is filled in with macOS automatic translation. It is not attached to lines that are already Korean.
- If the lyrics server refuses a request, "Will not request again for about N minutes (약 N분 동안 다시 요청하지 않습니다)" — after that time (10 minutes, or 1 hour depending on the kind of refusal), it searches
  again from the next track. If you turn lyrics search off and on in Settings, it is released immediately.
- A track that was not found is not asked about again for **30 minutes**, and a track for which the server did not respond, for **2 minutes**. After that, playing the same track again or opening the lyrics panel searches again.
  Refresh (↻) searches once more at any time.
- Even if a track's name is written differently in each playback app (a Korean artist name in Apple Music, "- Remastered 2011" in Spotify, the album's
  "- EP"), it is found if it is the same track — the title and length (±3 seconds) must be the same and one of the artist or album must overlap. Someone else's
  track with only the same title and length (a cover, etc.) is not shown.
- If the lyrics of the same track are posted separately as the original · romanized pronunciation · translation, **lyrics written in the same script as the track title (Japanese · Korean · Chinese) are
  shown first**. If the title is only English letters, the best-matching lyrics are shown as before.
- **Lyrics edition** (the book-shaped button under the lyrics): choose among the editions found (Japanese (original) · romanized · English · Korean, etc.) to switch. The chosen edition applies only to this track and
  is remembered. If there is only one edition, **Find another edition (다른 판 찾기)** searches once more.

### 2.4 Menu bar icon · menus

- **Menu bar icon** (a waveform): a status line · Start · Stop · Play/Pause · Open Window · output device name · **EQ preset ▸** (the latest five — choosing one is heard immediately and
  is not saved, §6.2) · Quit Fidenne. Start · Stop are the same as the engine switch (Start does not play a track — §2.2).
- **Hiding the icon**: macOS does it — if you turn off Fidenne in **System Settings › Menu Bar › Allow in the Menu Bar**, the icon disappears,
  and if you turn it on again, it returns. The app does not put the same switch inside itself (if it were turned on and off separately in two places, it would be unclear which side won).
  Even if you hide the icon, the window · Dock · shortcuts stay as they are.
- **App menu (Fidenne)**: at the bottom of the "About Fidenne (Fidenne 에 관하여)" window there is a trademark notice — one line saying Apple Music · Spotify · YouTube Music are trademarks of their respective companies and Fidenne has no relationship with them. Right under "About Fidenne", **Check for Updates… (업데이트 확인…)** — only when you press it, it reads the public repository's latest release once
  and reports "You are up to date (최신입니다)" or "New version x.y (build n)". If there is a new version, for an install through Homebrew, **Copy command (명령 복사)** for `brew upgrade --cask fidenne`; for an install from the .dmg,
  **Open the release page (릴리스 페이지 열기)** (in the browser). The app does not check, download, or install by itself.
  If the public repository has no release yet, it reports "No release has been published yet (아직 공개된 릴리스가 없습니다)" (this is not a fault). In a
  build made without a public account, it is off with "Update checking turns on after the public repository exists (업데이트 확인은 공개 저장소가 생긴 뒤 켜집니다)".
  What goes out is the `github.com` line in [Privacy document §3](../../../PRIVACY.en.md) — it can be turned off in Settings › Privacy › Network destinations.
- **Playback menu**: playback actions and "Shortcut Settings… (단축키 설정…)".
- **The shortcut list** is on the **Controls and Shortcuts** tab of the Settings window — open the window with ⌘, · the app menu's "Settings…" · the **Settings…** at the very bottom of the sidebar, and choose that tab.
  "Shortcut Settings…" at the end of the Playback menu opens that tab directly.
- **Help menu**: Show Controls (조작법 보기) · [Released build] **Create Diagnostics for Problem Reports… (문제 제보용 진단 만들기…)** (§10).
- **Diagnostics menu**: start/stop diagnostic recording (released build, local only) · [Dev build] "Mark Problem Occurred (문제 발생 표시)" · **Export Diagnostics for Support… (지원용 진단 내보내기…)** ·
  **Delete Saved Diagnostics… (저장된 진단 삭제…)** — it cannot be undone, so it asks once (the same button on the Development page asks the same question).
- **Deletions that cannot be undone ask once**: deleting saved diagnostics · deleting a playlist · shortcuts "Reset All to Defaults (모두 기본값으로)". The question window closes with **Cancel** or
  **Esc**. **Delete** (for shortcuts, **Reset to defaults (기본값으로)**) is in red text and is not pressed by Return.
- **Settings window (⌘,)**: at the very top, an info line with the edition number (`Fidenne 0.4.x (build n)`) and **Check for Updates…** (the same as the app menu). Under it, the shortcut list. For each key: change · clear · default; "Reset All to Defaults…" (after asking); the skip interval for forward/back. If it overlaps a macOS shortcut, it
  tells you, and if it is a key another action was using, it asks whether to move it. It works only while the window is in front (if another app is in front, only the media keys).
  **Toggle Blind mode (블라인드 켜고 끄기)** remains in the list but a key cannot be assigned — because there is no screen that draws the blind display (the blindfolded comparison is ABX in the DSP page's A/B).
  When a shortcut ends up doing nothing, the reason appears on the DSP page's status line — A/B switching (when the two slots do not exist) · Next suggested filter (while playing or while the filter is
  being prepared) · Next saved sound preset (when nothing is saved).
  **Toggle EQ (EQ 켜고 끄기)** (the key · the Playback menu · the control channel `eq-enabled`) is the same as **EQ On** on the DSP page — it is heard immediately and is **not saved**.
  Even if the DSP page has unsaved EQ edits, this key does not save them. To keep them, Save on the DSP page (⌘S).
  **⌘S (save EQ · Ostrum)** is also in this list — it works even with the Korean input method active, and can be changed to another key. It saves the Equalizer or Ostrum that is on the screen,
  and if there is nothing to save (the Save button is dimmed), it does nothing.
  **⌘F (search)** goes to **that page's search field** on the Library · Listening History pages (and, if an album · artist · playlist is open, returns to that list first),
  and on other pages goes to the Music page's search field.

### 2.5 Explanations · how to read graphs · glossary

Feature explanations have the **same frame** on every page.

- The one line directly under a section title is **what this feature does**. Clicking the **ⓘ** at the end of that line (with the keyboard, put focus on ⓘ and press Space) opens a
  bubble (popover) on the spot that shows When do I use it? (언제 쓰나요?) · What do I put in? (무엇을 넣나요?) (the format, for a file) · What changes if I change it? (바꾸면 무엇이 달라지나요?) · Cost (대가). It does not
  open merely from hovering the cursor. **Esc** or clicking outside the bubble closes it. The bubble does not exceed half the window's height, and overflowing text scrolls inside the bubble.
  Clicking ⓘ does not push the controls beneath it.
  Long answers such as "What changes when the filter length increases? (필터 길이가 늘어나면 무엇이 달라지나요?)" · "Why are there three gain controls? (이득 조절이 왜 셋인가요?)" are also opened with the ⓘ beside the question.
- **What is visible without clicking is up to the name · state · one line**.
  An explanation longer than one line is in the **ⓘ** at the end of that one line: where a feature's "What does it do? (무엇을 하나요?)" ran over two lines (Output mode · DAC format check · Input and output devices ·
  Playback Chain · Filter · DSD conversion · Buffer · PCM headroom · Sound preset), a short single line remains and the original sentence moved to the bubble's first line, **What does it do?**.
  The two- or three-line notes under a control (autoplay · tap target and recording permission · 7th/5th order · experimental dither · start rate · buffer set · headroom adjustment · interface scale ·
  Liquid Glass · playback capsule material · haptics · when lyrics search is off · genre and tempo values · app queue · playback position · when shortcuts work) are the same — the text is unchanged, in the bubble.
  The **Listening History** page has an ⓘ at the end of the subtitle in the window header (the first line of the page that repeated the subtitle was removed).
  **The DSP page is the same**: for Equalizer · EQ Backend · Ostrum · Crossfeed · graph editing · Auto fit · measurement · target file · clipping ·
  LLM polishing · A/B · ABX · the excessive-setting detector, the "What does it do?" is left as one line and the original text moved to the bubble's first line. The note under the band row · the
  measured values of Linear Phase Length · what the LLM prompt contains · the conditions of Loop Comparison · how to read measurements · target files are also one line + ⓘ. How to handle the Ostrum knob (turning · vertical dragging ·
  Shift/⌥ · double-click) and the numbers of the Harmonics provisional values are inside the ⓘ (What do I put in? · Cost) in the Ostrum header.
  Warning · error sentences, and consent sentences that say what goes out, are unchanged and always visible. Development information such as decision numbers · identifiers is not used on the screen.
- Clicking **Glossary (n) (용어 풀이 (n))** inside an explanation shows that part's terms one line at a time, and **View the whole glossary (용어집 전체 보기)** shows the whole of the app's glossary (SRC · taps · passband ·
  transition band · image · linear phase · minimum phase · ringing · delay · dB · DSD · modulator · headroom · crossfeed · M/S · Q · target ·
  loudness · ABX, etc.). The meaning of a term lives in this one place only.
- The numbers are carried over from measurement tables, and where there is no measurement, it says there is none. It makes no judgment that any explanation makes the sound better.

**How to read graphs** — directly under each graph, two lines of **horizontal · vertical (units and the meaning of the reference line)** and **lines · name · name …** (the names of the lines the graph draws) are
always visible — because they are needed while looking at the graph. Clicking the **ⓘ** at the end of those lines shows in a bubble **what each line is** (the long meaning), **how to read it**, and **what this graph cannot tell you** —
because the legend and axis names are needed while reading the graph, and the explanation only when you decide to learn. The color of a line is in the graph's own legend.

| Graph (page) | Horizontal | Vertical | Lines · bars | How to read | What it cannot tell |
|---|---|---|---|---|---|
| Filter frequency response · full view (I/O → Currently selected guide) | Frequency 0–30 kHz | Magnitude dB (0 to −160), 0 dB = same magnitude as the input | The selected filter · the 0 dB line | Where it sits on 0 dB, it passes as is; from where it bends down near 20 kHz, it attenuates. Above 22.05 kHz, how much it cuts the images (ultrasonic afterimages) | Phase · ringing · delay · audible quality, the DAC output |
| Filter frequency response · transition band comparison | 18–22.5 kHz | Magnitude dB (0 to −40), −6 dB ≈ half the amplitude | The selected filter (solid) · **Linear Reference = the response of the default filter (short linear phase), the comparison baseline (dotted)** | If the solid line drops at a lower frequency than the dotted line, it attenuates near 20 kHz earlier, and if steeper, the transition band is narrower. Dropping lower is not a better sound | Phase · ringing · delay · audible difference |
| Response (DSP) | 20 Hz–20 kHz logarithmic | Magnitude dB, dark line = 0 dB (measurement · target are shifted to 0 dB at the reference point) | Target · my headphone · after correction (the darkest line) · EQ curve · show more (EQ + Ostrum · Ostrum) · being edited (thick solid line while turning off) · EQ R channel · blue dots (bands — drag to edit) · red dotted line (GraphicEQ fit error) · red segments (excessive boost) · a faint spectrum behind | The closer the after-correction line sits to the target, the better the match. If the EQ curve is above 0 dB, it boosts that band. With Target flat, the closer the after-correction line is to 0 dB, the closer it is to the target | Phase · delay · harmonics · dynamics · fit differences · sound quality |
| Spectrum (DSP — faint behind the Response graph) | Same frequency as the graph above | dB −100 to 0 (the graph's bottom to top, separate from the graph's dB axis), 0 dB = full-scale sine | Post-DSP curve (fill, default) · pre-DSP (cyan line) · peak (thin line) · A/B previous slot (faint orange line) | A high place = a band with much musical energy; the difference between the fill and the cyan line = as much as the DSP changed (including volume) | Sound quality · source resolution · differences between 1/24 bins below 47 Hz (narrower than the window) |
| Crossfeed M/S (DSP) | 20 Hz–20 kHz logarithmic | dB | Mid (L+R, 0.00 dB horizontal) · Side (L−R) | As much as Side goes down, the left-right difference is reduced | Phase · sense of space |
| Composite Response (Ostrum) | 20 Hz–20 kHz logarithmic | dB (3 dB steps) | M (solid) · S (dotted) | Above 0 dB = a band Ostrum boosts; if S > M, the width gets wider | Sound quality · volume change (for comparison, Auto Bypass) |
| Before and after (excessive-setting correction) | 20 Hz–20 kHz logarithmic | dB, red line = 0 dB | Before correction (dotted) · after correction (solid) · 0 dB line | If the after-correction solid line is under the red line, the maximum gain does not exceed 0 dB | Harmonics · dynamics · limiter |
| Playback trend (Listening History) | Date — one bar = 1 hour in the 1-day view · 1 day for 1 week/1 month · 1 week for 6 months · 1 month for 1 year | Play count (times) | Service color | Clicking a bar shows that bar's count | Actual listening · while the app was closed |
| Where did you listen · Most listened artists · Genre · Tempo (Listening History) | Ratio (%) · count (times) · tempo (BPM four bins) | — · artist · genre · count (times) | Service color · bars | The longer (higher), the more listened | Per-track breakdown · the same artist written differently · a verdict on taste · time listened |

### 2.6 Handling knobs · sliders · EQ points

**Controls tip.** When you first open the DSP page's **Equalizer** (the band row) and **Ostrum** (the knobs), the macOS standard **tip** speech bubble appears once beside that control
(Apple TipKit). If you close it with **✕**, it does not appear again. To see it again:

- Menu bar **Help › Show Controls (도움말 › 조작법 보기)** — opens a **Controls** window with the same content as the table below.
- The **ⓘ** beside the control — for the Equalizer, at the end of the one line under the band row; for Ostrum, at the end of the description line in the header (What do I put in?).
- In **Settings › Controls and Shortcuts › Controls** line, **Show the tip again (팁 다시 보기)** — after that, if you open the Equalizer · Ostrum again, the tip appears once more.

How to tell it worked: when the tip appears, the speech bubble's title is **Handling the EQ (EQ 다루기)** · **Handling the knob (노브 다루기)**. After closing the tip, **Show Controls** is in the **Help** menu.

| Action | How |
|---|---|
| Knob (Ostrum) | Turn it as if drawing a circle, or drag the center straight up and down (dragging up makes it larger). You can also put the pointer on the knob and, holding **⌘**, swipe up and down with two fingers. Holding **Shift** or **⌥** gives fine adjustment. **Double-click**, or **press once holding ⌥** (without dragging), for the default; clicking the knob's number lets you type it in |
| EQ slider | It jumps to where you click, and you drag to raise and lower while holding. Put the pointer on it and, holding ⌘, swipe with two fingers to move it in 0.1 dB steps (usually 0.5 dB per 6 pt; adding Shift · ⌥ makes it ten times slower). **Double-click** or **⌥-click** sets 0 dB (Preamp too). To return the whole band to its initial values, **Reset Band** |
| EQ number field | Click to type and press **Return**. The arrows beside it move one step at a time. You can also swipe with two fingers while holding ⌘. For the gain · Preamp · Q fields, **⌥-click** sets 0 dB · that type's default Q (the frequency field has no default). Double-click selects a word, as a text field does |
| Point on the graph (EQ) | Dragging changes frequency and gain together. Dragging while holding **Shift** or **⌥** is ten times slower (the same fine-adjustment keys as knobs · sliders). **Clicking a point makes it the selected point** (an outer ring), and while holding **⌘**, swiping up and down with two fingers changes the gain, and swiping sideways changes the frequency (release by clicking an empty place or Esc). If it is not selected, or without ⌘, the page scrolls. Dragging the small ring beside the selected point sideways also changes Q. Double-clicking an empty place creates a band there |
| Other sliders · playback bar | Click or drag, and while holding ⌘ swipe with two fingers to move one step at a time (PCM headroom 0.5 dB, playback bar 1 second — the playback bar moves once when you stop swiping) |

**When two-finger scrolling changes a value.** Two-finger scrolling always moves the page, and a value changes only when you scroll **while holding ⌘**.
Scrolling over a control without ⌘ briefly shows "Scroll while holding ⌘ to adjust the value" beside it. Pressing and dragging always works.
Moving your fingers up makes the value larger (following the system's scroll direction setting). In **Settings › Controls and Shortcuts › Change values with two-finger scrolling**, you can choose
**When started over a control** (without ⌘, when you move the pointer into the control and then scroll — the old rule) or **Off** (scrolling is always the page's). EQ · Ostrum are heard immediately when changed, and to keep them for the next launch too, save (⌘S).

**Undo one step at a time with ⌘Z** (macOS's Edit › Undo · Redo). What you changed on the DSP page is undone
one step at a time with **⌘Z** (Edit › Undo) and redone with **⇧⌘Z** (Redo). The undone value is also heard immediately — it goes to the engine by the same path as when you change it by hand.

- One step: **everything from one press-and-drag** (the dozens of changes while dragging a point · slider · knob are one step), **one ⌘ scroll** (until you lift your fingers or the wheel pauses),
  one number entry (Return), one switch · button. The Edit menu says what it will undo — for example: `EQ Gain (EQ 게인)` · `EQ Band Move (EQ 밴드 이동)` · `Add Band (밴드 추가)` ·
  `Preamp` · `Ostrum Headroom` · `Crossfeed`. The menu's leading word (Undo / 실행 취소) follows the app's language.
- Whole-sale changes are also one step and are named: `Load EQ Preset (EQ 프리셋 불러오기)` · `Auto fit` · `Reset EQ (EQ 초기화)` · `Graphic 31` · `Load EQ File (EQ 파일 불러오기)` · `Correction Strength (보정 강도)` ·
  `Excessive-setting correction (과한 설정 보정)` (apply correction · revert correction · all Preamp reductions made by Prevent clipping) · `Revert to Saved EQ (저장한 EQ 로 되돌리기)`.
- Values changed by the engine or elsewhere (the menu bar · a shortcut · the control channel) are not a step — counting starts again from there.
- You can undo even after going to another page and coming back, and after saving (⌘S) (it disappears when you quit the app). If you are typing text in a number field, ⌘Z undoes that text first (the macOS default).
- The header's **Revert to saved (저장본으로 되돌리기)** remains as it was — if ⌘Z is one step back, this goes **to the last saved state** at once (this too can be undone with ⌘Z).

### 2.7 Track menu — ⋯ and right-click

Where a track appears as one row (the Music page's tracks · the Up Next list · the Library's songs · albums · artists · playlists · Listening History), pressing the **⋯** at the end of the row or
**right-clicking** the row (Control-click · two-finger click) shows **the same menu**. The bottom bar's ⋯ uses the same order. The items are always in this order, and
items that cannot be done on that row are not dimmed but **left out** (a row with nothing to do has no ⋯ either).

1. **Play** · **Play Next** · **Add to End of Queue** — the latter two appear only when a list is playing in Fidenne (Music page).
2. **Add to Playlist ▸** (a Library track, when a playlist exists) · **Show Lyrics** · **Track Info** (bar ⋯) · **Link with the same music on another service… (다른 서비스의 같은 음악과 연결…)** (Music page) ·
   **Open in Apple Music** (store track) · **Show in Playback App** (bar ⋯) · **Show in Finder** (Library file) · **Copy Link** (the web address of a store track).
   If there are two or more places to open it, they are grouped into one **Open in Another App ▸**.
3. **Remove from Playlist…** (after asking — the file stays as it is) · **Remove from Queue** (the Next Up of a Library file — does not ask).

Spotify tracks (including the Spotify rows of Listening History) have **Open in Spotify** (browser — the Spotify app receives it and opens it) · **Copy Link**. Selecting several tracks at once is not yet possible.

## 3. Music page

The place to search and open Apple Music · Spotify · YouTube Music in one place.

- **Service list**: pressing the service button before the search field shows **Apple Music** · **Spotify** · **YouTube Music** always in this order, with a ✓ on the one now chosen.
  If YouTube Music is not connected yet, "Not connected (연결 안 됨)" is attached beside the name and **Connect YouTube Music… (YouTube Music 연결하기…)** is under it. For the YouTube Music side, §8.1.

- **Search**: "Search tracks · artists · albums · composers (곡·아티스트·앨범·작곡가 검색)" / "Search from my list to all of Spotify (내 목록부터 Spotify 전체까지 검색)". Search shows the results of only the one service now chosen — to see another service's results, switch with the service button before the search field (when you switch, that service is searched then). A service app's icon is shown without cropping, together with its name (at least 30 pt even when small), and the head of the iTunes Store results does not borrow an icon.
  Suggestions below the query expand within the panel even when the search field is narrow. Each title and artist uses one line, as does the service heading. Available search-result artwork is shown; otherwise a music symbol appears. The album-view search panel works the same way — the suggestion panel of its header search field also shifts left to stay inside the window.
  When you scroll, the search field rises to the head.
- Opens **my playlists · library albums (saved albums)**, with back/forward (horizontal swiping — following **System Settings › Trackpad › More Gestures › Swipe between pages**; among two fingers · three fingers · off, as you chose, and whether it goes is decided by macOS from how fast your hand is), and refresh.
  When the window is narrow, button names get shorter — My Playlists → Playlists, Library Albums → Albums, Auto Linking → Linking (VoiceOver reads the long name).
- Clicking a track gives the **playback method**: Play Next / Play Now. The ⋯ at the end of the track row or right-click: the track menu (§2.7 — Play · Play Next · Add to End of Queue ·
  Link with the same music on another service…).
- **Play All · Shuffle**: a pass through the list with no duplicates. Long playlists draw only rows near the visible area to reduce display work.
- **Spotify connection**: enter the Spotify Client ID and connect (do not enter the Client Secret). After connecting, "Refresh playback permission (재생 권한 갱신)", "Disconnect (연결 해제)".
  **Follow Spotify queue · for Jam (Spotify 대기열 따르기 · Jam용)** — when on, Fidenne does not overwrite the Spotify shared queue (start the Jam in Spotify).
- **Auto Linking · Music Linking Review (자동 링킹 · 음악 링킹 검토)**: looks up the unlinked tracks of the two services and makes **candidates only**. Until approved, they are not merged into the statistics.
  Link confident candidates · link / exclude / re-review · external review (export a JSON review package · import results · copy review instructions).
- The Apple Music library is read all at once if you allow the MusicKit permission, and if you do not allow it, it is read through the Music app.

- **Music home** (Apple Music · Spotify): **Resume**, **Today's listening** (or **Recent listening**), **My playlists**, and **Rediscover**. Scroll the page vertically to see all loaded items in My playlists and Rediscover. The number of playlist columns follows the window width. Home loads up to 24 playlists and 12 albums. Use **My playlists › All (내 재생목록 › 전체)** to see more playlists. Rediscover is a selection of albums, not the entire library.
  **Resume (이어 듣기)** targets the service and track shown on the card. If another service or a local file is playing, it selects the card's track. For a card from a list managed by Fidenne, if the same track from the same service is current and no saved playback position applies, it plays or pauses that track. If a saved position applies, it resumes from there.
  If the app can open the list the card's track was heard in (playlist · album · liked songs · a Fidenne list · an imported YouTube Music list), a **Open list (목록 열기)** button appears next to ▶ and the heading reads `Resume (이어 듣기) · list name` — the same for Apple Music, Spotify and YouTube Music. For a track with no list on record (Heard today · search · a single track), the app looks for a list among My playlists that holds the track, and shows no button if none does.
  Pressing the card's **cover** opens the large playback view (album view) — it does not start sound (playback is ▶). It opens only for the current track; the cover of a card made from listening history does nothing.

**Playing an Apple Music playlist**: track information appears as each part is read. Selecting **Play All (전체 재생)** or a track requests playback only after the list has been read to the end. To mix the order, turn on **Shuffle (셔플)** before selecting playback. **Shuffle** alone does not start playback. The first uncached read may show **Preparing playback… (재생 준비 중…)**; existing playback and the queue remain in place while you wait. A fully cached list requests playback without waiting to read it again. If the app reports that it could not read the list, select the playlist again, or use **Refresh list (목록 새로고침)** (↻) and select playback again.

## 4. Library page

The music files on this Mac. It has **the same look as the Music page** — on top the search field and the **Music folders (음악 폴더)** menu, under them **Songs · Albums · Artists · Playlists (노래 · 앨범 · 아티스트 · 재생 목록)**,
above the list **Play All · Shuffle**, and for each track the cover · title · artist · album · format (FLAC · 96 kHz · 24-bit) · length.
The formats it reads are WAV · AIFF · FLAC · ALAC · AAC · MP3 · Opus (`.opus`). Opus plays only when macOS can read Ogg; on a macOS that cannot, that row shows
`Opus 를 읽을 수 없음` (cannot read Opus). `.ogg` and `.oga` files are not played yet.

- **At the start (no folder)**: one sentence and a single **Add Folder… (폴더 추가…)** button.
- **Music folders** (the menu beside the search field): Add Folder… · Re-index · Remove folder from list ▸ (removes only from the list, and the files on disk stay as they are). While removing, that folder stays in the menu as "— removing (— 빼는 중)" and you can keep using the window. If it cannot be removed, the folder stays in the list and the warning line above says why — try removing it again after a moment. Files are neither moved nor changed.
  Indexing in progress · warnings appear on one line under the search field.
- **Songs**: search by title · artist · album · file name (⌘F goes to this field — the search filters the list now visible). Clicking a row plays from that track.
  For each track ⋯ or right-click — the track menu (§2.7: Play · Play Next · Add to End of Queue · Add to Playlist ▸ · Show in Finder).
  For a file that cannot be played, the reason (such as `Corrupted file (손상된 파일)`) appears in the format place and it cannot be clicked.
- **Albums · Artists**: grouped by tag (if there is no album tag, `No album info (앨범 정보 없음)`; if there is no artist, `No artist info (아티스트 정보 없음)` — it does not guess from the file name).
  Clicking one opens that album (in disc · track order) or that artist's tracks, and **‹** (list back) returns. The row's ⋯ plays all of it · plays it next · adds it to the end of the queue · adds it to a playlist.
- **Playlists**: enter a name and create → that list opens. Inside a list: Play All · Shuffle · Delete… (after asking — the playlist only, the files stay as they are) · per track move up/down ·
  the track menu's "Remove from Playlist…" (after asking). A "File not found (파일을 찾을 수 없음)" row means the folder was removed or the file was moved.
- **Selecting several tracks · dragging to reorder** (inside a playlist · the Next Up pane): clicking a row alone plays from that track, as it does now.
  **⌘-click** adds or removes only that row, and **Shift-click** selects from the last clicked row to here (⌘ + Shift adds). Selected rows are shaded lightly.
  If you **drag a row onto another row**, it moves to that place — if you drag a selected row, everything selected goes together in order (dropping it lower puts it after the row you dropped on, and dropping it higher puts it before).
  **Return** plays the first of the selected tracks. The move up/down buttons remain as they were, for the keyboard · accessibility path.
  A track that the engine has finished preparing to play next cannot be moved (moving it shows "The engine has already finished preparing this track to play next… (엔진이 이미 이어 재생할 준비를 마친 곡…)").
- **Play All · Shuffle**: Play All plays in order (turning shuffle off), and Shuffle turns shuffle on and starts from any track. It is the same state as the bottom bar's shuffle button.
- **Next Up (app queue)**: when a Library file is playing, the **Next Up** pane (the bottom bar's list button) shows the app queue — Now Playing · upcoming tracks ·
  Clear (from the next track) · per-track move up/down · ⋯ (Play · Show in Finder · Remove from Queue). **Tracks of the same sample rate play on without a gap, and where the
  rate changes, the output is reopened and there is a brief gap.** Tracks that could not be played are shown dimmed. If you play streaming, that pane returns to the streaming queue.
- Play · pause · previous · next · position · shuffle · repeat are done by the **bottom playback bar** (the separate playback bar the Library page used to have was removed). Moving the position reopens the output and there is a brief gap.
- Files are played **through the engine**. Even when it is set to PCM Direct, local files go out through the engine's PCM output.

YouTube Music playlists gather into one list not on this page but at `Music › YouTube Music › My playlists (내 재생목록)`. There are two ways to bring them in —
lists opened in the browser (§8.1; if the extension is connected, by opening a list screen in YouTube Music), a Takeout file (§4.1, no internet request). A list opened in the browser has `From the browser (브라우저에서)` and the received time at the top and is removed with **Delete…**. The Albums · Artists screens of the YouTube Music library are received too when you open them yourself in YouTube Music (§8.1) — the received screens show as **Albums** · **Artists** rows and are removed with **Delete…** (the YouTube Music library itself stays as it is). Fidenne does not walk around the YouTube Music site by itself. Tracks that came from Takeout · the account use the same kind labels · the same include/exclude ·
the same track menu, and what I chose for each track is stored in one place.

**What you can do on a track row** (both ways)

- **Kind (종류)**: each track is seen as one of song (a library song · an "Artist - Topic" channel) · `Music video (뮤직비디오)` (an official channel — a name ending in VEVO · "Official" · "공식" — or
  a music video with a record label rights notice) · `Music clip (음악 영상)` (other music videos — including music made with AI) · `Not music (음악 아님)` · `Kind unknown (종류 모름)` (no field to judge from)
  as one of these. By default **only `Not music` is left out of the list** and the rest go in.
- **Include · Exclude**: **Exclude (빼기)** / **Include (넣기)** at the end of the track row. Turning on **Show filtered-out items (걸러진 것 보기)** shows excluded tracks too so you can include them. What you chose is saved and
  **stays as it is after re-importing · refreshing · relaunching the app · the judging rules changing**. The ✕ on a row you chose yourself erases my choice and returns it to the judgment.
- **Track menu** (⋯ or right-click, §2.7): **Open in YouTube Music** · **Copy Link** · for an excluded track, **Add to Playlist ▸ that list**, for an included track,
  **Remove from Playlist…** (asks once — it can be returned with Include). If the Chrome extension (§8.1) is connected, Open plays right away in the YouTube Music tab,
  and if not, it opens the track page in the browser.
- **Found in another app (다른 앱에서 찾음)** (a link mark): when exactly one track already known in Apple Music · Spotify has the same title and an overlapping artist, it is linked with that track.
  The ISRC (the international number attached to each recording) lookup is not done at import time but when that track is played.
- The tracks in this list are not played inside Fidenne — because they are YouTube Music videos. The track's name and pairing remain in the track identity record used by lyrics · Listening History.

### 4.1 Importing YouTube Music playlists

Import the playlists you made in YouTube Music and your library songs from the CSV files of **Google Takeout** (Google's download of my data).
Fidenne **asks the internet nothing** — it reads only the files I received.

1. Open `takeout.google.com` in the browser and log in with a Google account.
2. **Deselect all** → in the list, check only **YouTube and YouTube Music**.
3. Click **All YouTube data included** on that line and leave only **playlists** and **music** (library songs). The names may differ slightly depending on the account language.
4. **Next step** → export once · file type `.zip` → **Create export**. When it is ready, an email arrives — download from the link.
5. Double-click the downloaded zip in Finder to unpack it.
6. In Fidenne, at the bottom of `Music › YouTube Music › My playlists (내 재생목록)`, expand **YouTube Music library (YouTube Music 보관함)** and press **Import YouTube Music playlists… (YouTube Music 재생목록 가져오기…)** → choose the unpacked folder (`Takeout`) as a whole, or choose a CSV file.

After importing, it tells you in one line — `N playlists · M tracks · music K · found in another app L (재생 목록 N개 · M곡 · 음악 K · 다른 앱에서 찾음 L)`.

- **Names**: the playlist file has only video numbers and no track names. If you also choose the **library songs** file of the same export (it happens by itself if you choose the whole folder),
  those tracks get names. Those whose names are unknown are shown as `Item with unknown name (이름 모르는 항목)` rows.
- Takeout playlist files have no channel · category, so most go in as `Kind unknown`.
- Importing the same playlist again **overwrites it** (it does not become two copies). **Delete…** removes only the lists imported into Fidenne.

## 5. Listening History page

Plays recorded on this Mac. What this page counts is in the ⓘ at the end of the window header's subtitle. **It does not upload automatically** — you can export by hand as JSON/CSV.

- Period: 1 day · 1 week · 1 month · 6 months · 1 year. **Source**: All · Apple Music · Spotify · Local (Library files). Graphs: **Playback trend ·
  Where did you listen (Apple Music · Spotify · Local) · Most listened artists · Genre and tempo**. If you choose a source, the export is also only that source.
  When the window is narrow, the buttons that choose the period and source become pop-up menus (what can be chosen is the same).
- **Files played from the Library** are counted by the same standard. The record keeps only the file's title · artist · album tags and an **identification hash** made from the file path
  (`local:…`) — **the file path · folder name · file name are not kept.** For a file with no title tag, the file name is shown during playback, but
  the record keeps it without a title and shows it as "No title (제목 없음)". A local track is not a target for linking between services.
- **The standard for one play**: real playback progress detected while Fidenne is open of 30 seconds or half the track's length, whichever is shorter. Seeking · pausing excluded.
  **It is not proof of actual listening or of audio output, and there is no record from while the app was closed.**
- **Per-track record**: track · artist · album filter (⌘F goes to this field), counting linked tracks heard on two services together, "Link candidates (연결 후보)" (those that look like the same track)
  link / no. A song you played on both Apple Music and Spotify is shown as one line with the total and the count per service (for example Apple Music 8 · Spotify 3),
  and what the merge rests on (matching ISRC (ISRC 일치) · confirmed by you (직접 확인)). Only a matching track ID (ISRC) merges by itself. Songs whose title and artist names merely look alike
  appear as a link candidate only, and are merged once you press **link** (Live · Remix · language versions with a different version mark are not offered).
  Merging never changes the saved play records (the merge happens when the records are counted).
- Export: JSON (including the aggregation standard) · CSV (1 row = 1 play). If you turn off "Save listening history on this Mac (이 Mac에 청취 기록 저장)", it does not record.
- Genre · BPM use only the values the playback app gave (there is no Spotify BPM, and the genre · BPM of Library files is not yet recorded). Missing values are not estimated.

## 6. DSP page

Header: `DSP` · input rate (`Input 44,100 Hz`;
when stopped, "재생 전 · 44.1 kHz 기준 (마지막 재생)" (Before playback · based on 44.1 kHz (last playback)) or "재생 전 · 48 kHz 기준 (재생 기록 없음)" (Before playback · based on 48 kHz (no playback history))).

On this page the **terms** (Response · Target · Headphone · Final · Add Band · Graphic 31 and so on — the names of buttons, layers, and fields)
are in English, and the **sentences** (guidance, warnings, status) are in Korean. The Ostrum panel and the Auto fit · clipping · A/B · ABX areas are
the same. Values and states (켜짐 (On) · 꺼짐 (Off) · 처리 (Processed) · 원본 (Original) · 아직 측정하지 않음 (Not measured yet) and so on) and the Cancel · OK of dialogs (취소 · 확인) stay in Korean.

**Top to bottom** (under the graph and spectrum come the EQ · Ostrum · Crossfeed picker, then the detailed settings — an order fixed by the screen rules):

1. Header — the rate, next to it the **last notice line** (there is always room for two lines, so the page does not move when a notice appears), and at the end of the line a small **A/B button**.
   The button text says what is running — normally `A/B`; during a comparison `A/B · B 듣는 중` (A/B · listening to B) · `Auto Bypass · A 듣는 중` (Auto Bypass · listening to A) (with ` · Loop` appended for Loop); during ABX `ABX 3/8`.
2. **A/B panel** (only when you press the button; directly under the header — it is inside the page rather than in a window, so you can keep it open and touch the EQ under it): A · B save · request ·
   Start A/B · Start Auto Bypass · level-match badge · one status line, and after that the slot values · Level Match · ABX · Auto Bypass interval · Loop (§6.7).
3. **Response card** (§6.1) — the graph with the **spectrum faintly laid behind it**, one row of Spectrum controls (and its one status line), one legend row (layers on/off), the excessive-settings detector,
   and the collapsible section **How to read the graph · notes (그래프 읽는 법 · 주석)** (the Preamp-subtracted line · axis reference point · graph notes · horizontal · vertical · what each line means — moved so the first view of the default window fits, with the content unchanged).
4. The tab strip **Equalizer · Ostrum · Crossfeed**, and under it the details of the chosen one. Inside Equalizer, directly in front of the band columns there is one **Auto EQ row** — even when collapsed
   it shows the current fitting basis (my headphone → target · number of bands) and **Auto fit**, and pressing anywhere on the row expands Headphone · Target · Bands · Strength (§6.2 · §6.5 · §6.6).
5. At the very bottom, the collapsible AutoEq license section.

The explanation fields whose sentence changes with the selection (Presence Mode · Topology · the graph axis reference point · Treble · the "from the next playback start" line of EQ Backend · the notes under the graph)
**always reserve the height of the longest sentence** — changing the selection does not move what is under them.
Selected segmented buttons · checkboxes · sliders · filled buttons are **grey and white** — in both light and dark. Changing the accent color in System Settings does not change it. Purple is used only for Fidenne's own sound features (an enabled DSP chip, Ostrum, the chosen sound recommendation).

**Everything stays as it is when you visit another page and return**: the opened measurement and target files, Ostrum edits, the auto-fit result and its explanation, the layers, whether the Auto EQ row is expanded,
whether the A/B panel is expanded, and the headphone search (squig.link) all remain until you quit the app. **EQ is heard the moment you change it, and it remains for the next launch only when you save it (⌘S)** (§6.2).

### 6.1 Response graph

- **Four lines are always in the legend**:
  **Target (타깃)** (orange dotted line, the target file) · **My headphone (내 헤드폰)** (gray, the measurement file) · **After correction (보정 뒤)** (the darkest and thickest line = my headphone + EQ + Ostrum, on by default) ·
  **EQ curve (EQ 곡선)** (thin blue line, EQ only — the band dots sit on this line). Each line has its own color and shape (in More, EQ + Ostrum is a green dot-dash line and Ostrum is a purple dotted line).
  Turning an item off in the legend removes everything drawn for it — turning off the EQ curve also removes the band dots · Q rings · EQ R channel · the line while editing. Fitting the EQ means **bringing After correction onto the Target**.
  - The rest are in a single **More (더 보기)** menu at the end of the legend: **EQ + Ostrum** (the curve that adds the two corrections — when Ostrum is off it equals the EQ curve) ·
    **Ostrum** (Ostrum only). The number turned on is attached to the menu name ("더 보기 · 1" (More · 1)). The line while editing · EQ R channel · fit error · excessive sections are lines that appear on their own.
  - Without a headphone file, After correction cannot be drawn, so the **EQ curve becomes the thick line** (its color stays blue). With only the target missing, My headphone · After correction · EQ curve are drawn and the Target entry is dimmed.
  - Layer on/off is **one row directly under the graph** (the legend) — for each entry an on mark · the same line as in the graph · the name.
  - EQ + Ostrum = EQ (engine calculation, left channel) + the small-signal magnitude of the Ostrum center (L+R). Crossfeed does not change the center, so it is not included.
- **When you scroll, the graph shrinks and sticks to the top**: as you scroll the page down, the Spectrum row first
  slips under the end of the card, and then the graph shrinks by the amount you scrolled (320 → 128 pt) and stays pinned at the top of the window. The [Equalizer · Ostrum · Crossfeed] tabs and the band columns pass
  under it. Scrolling back up grows it along the same path. While it is shrunk, the dB scale labels appear every other one, and the Spectrum row's choices gather into a single **Spectrum**
  menu at the end of the legend. This is the same for all three tabs.
- **Dot ↔ band column**: pressing a dot in the graph scrolls the band columns sideways to that band and fills that column. Grabbing a slider in a band column
  draws that dot in the pinned graph larger and shows its value. Pressing a number field makes that band the selected dot of the graph.
  - **The curves are drawn without the EQ Preamp** (so the shape can be compared directly with the target). EQ · EQ Right · Final ·
    After correction · the line while editing (the draft's Preamp) are all the same. **The Preamp is still applied to the sound** — the first line of the collapsible **How to read the graph · notes** under the card
    states the current value, as in "그래프는 모양 비교를 위해 Preamp(-5.6 dB)를 빼고 그립니다 — 소리에는 Preamp 가 그대로 적용되어 있습니다" (The graph is drawn without the Preamp (-5.6 dB) for shape comparison — the Preamp is still applied to the sound)
    (when the Preamp is 0 or the EQ is off, the line is empty and only its space remains). In the actual sound the whole curve is lower by the Preamp.
    The excessive-settings detector and Clipping & Headroom count with the Preamp included (their sentences say "EQ(Preamp 포함)" (EQ (Preamp included))).
  - **Ostrum's Headroom · Output (flat gain) are subtracted in the same way** (the same principle as for the Preamp, applied to Ostrum). Ostrum ·
    EQ + Ostrum · After correction show the shape as it would be with Headroom · Output at 0 dB, and the same line states the values, as in "그래프는 모양 비교를 위해 Preamp(-4.0 dB) ·
    Ostrum Headroom(-6.0 dB) · Output(-3.0 dB)를 빼고 그립니다 — 소리에는 모두 그대로 적용되어 있습니다" (The graph is drawn without the Preamp (-4.0 dB) · Ostrum Headroom (-6.0 dB) · Output (-3.0 dB) for shape comparison — all of them are still applied to the sound). The sound ·
    engine · detector are unchanged. The small Composite Response graph on the Ostrum tab is also drawn **without** Headroom · Output, and the line under it states the values in the same sentence.
  - The EQ · Ostrum curves are **what the engine calculated**. **They are drawn even when nothing is playing** — when stopped they are drawn at the last played rate (or
    48 kHz if there is none), and the first line under the graph says which rate, as in "재생 전 · 44.1 kHz 기준 …" (Before playback · based on 44.1 kHz …). If the playback rate differs,
    the highest octave may differ slightly. The Crossfeed window and the spectrum move only during playback.
- **View** (the segmented button in the card header): **Original** (the file · engine curves as they are) / **Target flat** (like the correction view of squig.link, the target as a 0 dB horizontal line —
  My headphone = headphone − target, After correction = (headphone + EQ + Ostrum) − target, and the EQ curve · Ostrum · EQ + Ostrum stay as they are). When there is no target,
  Target flat is not drawn, and the reason is shown at the start of the notes under the graph. With the pointer over the graph, both views also show the file's own value ("파일 N dB" (file N dB)).
- **Dots in the graph = bands**: for each enabled band on the Equalizer tab,
  a blue dot sits at **that band's frequency (horizontal) · gain (vertical)**. Dragging a dot changes both together and **you hear it immediately** (save with ⌘S, §6.2).
  - The pressable area is 24 pt per dot. When dots overlap, only one of the numbers remains (the selected dot always has its number) while both pressable areas remain — you can also select by the number in the band column.
  - The grabbed dot has a faint halo, a dotted circle at its original position while you drag, and at the top corner of the graph "밴드 4 · 1.20 kHz · −4.0 dB · Q 1.41 / 처음: …" (Band 4 · 1.20 kHz · −4.0 dB · Q 1.41 / Original: …) appears.
  - **Q**: drag the ring at the upper band edge of the selected dot (at half the gain height) sideways · or type into the Q field of the band column.
  - **Fine drag**: while dragging a dot, holding **Shift** or **⌥** moves the dot at 1/10 of your hand's motion (the same key · the same ratio as knobs and sliders). Pressing it in the middle of a drag does not make the dot jump. The old behavior of changing Q with an ⌥ drag is gone (in the app, ⌥ is always fine adjustment).
  - **⌘ swipe**: pressing a dot makes it the **selected dot** (the outer ring). Holding ⌘ and swiping with two fingers **up and down changes gain, sideways changes frequency** (one swipe follows only the direction it first moved, and ⌥ · Shift make it slower). Release by pressing an empty area or **Esc**; when released, or when swiping without ⌘, the page scrolls even over the graph. The old "scroll on a dot = Q" is gone.
  - **Double-clicking** an empty spot in the graph creates a band there (not when there are already 32).
  - When it differs from the saved value, a small empty circle sits at the **saved position** of the selected band.
  - While dragging (within the 50 ms before the engine catches up) the edit curve is a thick solid line and the engine's EQ is a dotted line.
  - **Curve mode is gone** — the 31-band graphic EQ is laid out as bands by **Graphic 31** (§6.2) in Equalizer. A GraphicEQ file
    (AutoEq · Equalizer APO format, a list of "frequency · gain" points) opened with **Open EQ Preset…** is immediately fitted by the engine into filters, placed in the band columns, and heard — the
    difference from the file stays as a red dotted line ("GraphicEQ 맞춤 오차" (GraphicEQ fit error)) until the next file. The number of filters is the same as Filters N of Auto fit.
- **Treble (Auto fit)** (in the collapsible **Advanced — files · treble · Generative AI (고급 — 파일 · 고역 · 생성형 AI)** inside the Auto EQ row — moved from the column beside the graph because it is a setting of auto fit): how to treat the treble of the correction that auto fit produces — correct everything (default) · no correction above a boundary (fades
  to 0 dB gradually; drag the **vertical bar** in the graph to set the boundary — it snaps near 12·14·16 kHz) · only half above 6–8 kHz · only a gentle
  trend above 6–8 kHz (3-octave smoothing) · no correction above 6–8 kHz. It is applied when you press "자동 맞춤" (Auto fit).
- **Graph axes** (the two menus Reference · Range in the card header, explained in the first line of the notes under the graph):
  - **Reference point**: 1 kHz (default) · 500 Hz · the 500 Hz–2 kHz average. The measurement · target files are shifted to 0 dB at this point and drawn on one axis with EQ · Ostrum · Final.
    The target has its slope added after the shift. Auto fit always fits at 1 kHz regardless of the reference point. So if you choose another reference point it may differ from the picture by a few dB (this is written under the graph).
  - **File values**: with the pointer over the graph, the pointer line shows the value of each layer. File layers also show the value before the shift (in the form `· 파일 88.4 dB` (· file 88.4 dB)).
  - **Range**: Auto (a 6 dB grid that contains all curves, at least ±12) · ±12 dB · ±18 dB · ±24 dB. A curve that exceeds a fixed range is clipped at the edge of the graph and
    `▲ 범위 위로 넘친 곡선이 잘렸습니다` (▲ A curve that went past the top of the range was clipped) appears (▼ for past the bottom, and `범위 위·아래로 넘친 곡선이 잘렸습니다` (A curve that went past the top and bottom of the range was clipped) for both).
  - The dark horizontal line is 0 dB (the scale label "0 dB" carries the unit; the horizontal scale is 20 Hz · 100 Hz · 1k · 10k · 20k (above 1 kHz, a short "k" as in graphing tools) with the faint 50 · 200 · 500 · 2k · 5k between, and in the top octave 12k · 14k · 16k · 18k — where you read where the source is cut off and the headphone's treble). The scale steps are the smallest interval among 3 · 6 · 10 · 20 dB that gives eight divisions or fewer.
  - When the graph is narrow, horizontal scale labels that would touch are dropped (the lines remain) — the decade labels (1k · 100 Hz · 10k) are kept first, then the two ends (20 Hz · 20k), then the in-between labels. The 12k–18k labels appear only when there is room (16k first when there is room, 14k if the window is a little wider) — even with no label the line is there, and the exact frequency appears when you hold the pointer over a curve.
  - The graph always uses the full width of the card (the side column is gone). The card header · legend · spectrum controls row wrap to the next line when they do not fit on one — even at the window size "Default" (920) and the minimum window, the page is not pushed out of the window.
  - Both choices remain for the next launch. Only the picture changes; the sound and auto fit do not.
- The **spectrum faintly laid behind** the graph: the per-band level of the sound being played, as a smooth curve —
  a full-scale sine in one band is at the very top of the graph (0 dB), and the very bottom is −100 dB. **The vertical scale is separate from the graph's dB axis** (the spectrum is music, not a response — the explanation line under it says so).
  The strip that draws only the spectrum has 100 · 1k · 10k labels and a faint 12k–18k line, and names only when there is room (16k first).
  The controls are the **Spectrum** row under the legend.
  - **View**: **After DSP (DSP 뒤)** (default — the sound that goes through EQ · Ostrum · Crossfeed · volume to the DAC, the filled curve) · **Overlaid (앞뒤 겹쳐)** (the After DSP fill + a thin teal line for the incoming
    original) · **Before DSP (DSP 앞)** (the original only). Lowering the volume also lowers the After DSP curve — it is the sound exactly as you hear it.
  - **Resolution**: 1/6 · 1/12 · **1/24 (default, 240 bins)** · 1/48 octave (479 bins). The narrower the bin, the longer the window with which the bass is read, so it responds later — at 1/24,
    below 95 Hz it is the average of roughly the last 0.74 seconds, and below 47 Hz even that window is wider than the bin so it moves together with the neighboring bins (at 1/48, below 93 Hz).
  - **Smoothing**: Fast 125 ms (default, like the Fast of a sound level meter) · Slow 1 s (Slow) · Off. **Peak hold**: a thin line holds each bin's maximum and falls at 20 dB per 1.7 seconds.
  - **Update**: 30 fps (default) · 60 fps. The engine computes the spectrum on its own thread (about 1 % of one core at 30 fps), and the drawing is composited on the GPU.
    When the panel is not on screen, the engine does not compute.
  - **During A/B comparison**: when you switch slots, the curve of the slot immediately before the switch stays as a faint orange line so it can be compared directly with the new curve (the line under it says "옅은 선: 슬롯 A 의
    마지막 곡선" (Faint line: the last curve of slot A)). The new curve takes about 0.1 second to settle in the treble and about 0.75 second at the lowest bass.
  - The line under the graph tells the reason for a stop: "엔진이 멈춰 있어 …" (The engine is stopped, so …) · "엔진은 돌지만 n 초째 캡처에서 소리가 오지 않습니다" (The engine is running, but no sound has arrived from capture for n seconds) · "스펙트럼 스레드가
    n 초째 돌지 않습니다" (The spectrum thread has not run for n seconds) — see the troubleshooting guide, 'The spectrum is frozen (스펙트럼이 멈춤)'.
- The **Auto fit** button is in ③ Auto fit of the **Auto EQ** tab of Equalizer. Pressing it fits right away — the result (N filters) goes into
  the band columns and **is heard immediately**, and under the button appears "필터 N개를 밴드 열에 넣었고 지금 들립니다 — 남기려면 저장(⌘S)." (N filters have been put in the band columns and are being heard now — to keep them, save (⌘S).) If it cannot fit, the button is disabled and
  the reason (choose the headphone measurement first · treble handling and so on) appears in orange under it. It fits any number of filters from 1 to 32 — the default 10 is AutoEq's configuration (low shelf ·
  high shelf · 8 peaking), other numbers add or remove peaking filters beside the two shelves, and 1 is a single low shelf. A GraphicEQ file is also fitted with the same number.
- **Excessive-settings detector (과한 설정 탐지기)** (one row under the graph): the status row keeps its height as values change. Its **ⓘ** opens findings, criteria, Prevent clipping settings, correction results and undo; **Suggest correction…** remains beside an excessive status. It **adds** the editor's current EQ (the value that will be heard soon, if you are dragging) and the **engine curves** of the Ostrum · Crossfeed held by the engine
  and looks for places beyond AutoEq's limits — a combined boost **above +6.2 dB** (AutoEq max gain +6.0 + 0.2 margin — per point below 10 kHz, the band average above 10 kHz)
  · whether that boost is an **overlap** of EQ and Ostrum · maximum gain **above 0 dB**
  (full-scale music would exceed 0 dBFS) · **a boost slope above 0 dB steeper than the flank of a single peaking filter placed there (Q 6 · +6 dB — the limit of AutoEq's fitted filters)**
  (about 32 dB/oct at 1 kHz, slightly steeper toward the treble) — **only when the curve of the boost part alone is that steep too** (a flank rising out of a cut
  belongs to the cut and is not looked for — the shape where Auto fit follows the side of a dip of AutoEq's correction curve is no longer warned about). In the ⓘ popover, when there is none, "탐지기: 과한 설정 없음 — 합성 부스트 최대 …" (Detector: no excessive settings — maximum combined boost …) appears;
  when there is, "탐지기가 과도한 설정을 찾았습니다 — '보정 제안…' 이 모두 고칩니다(…)" (The detector found excessive settings — 'Suggest correction…' fixes all of them (…)) appears (the promise is made only for what the correction can remove — what Ostrum created is stated separately as
  "EQ 보정으로 없앨 수 없어 그 탭에서" (cannot be removed by the EQ correction, so on that tab)), one line per finding (which frequency · the EQ share · the Ostrum share) appears,
  and a **red section** is drawn in the graph. It **does not block** — you can leave it as it is.
  - The reason the limits differ from AutoEq's numbers (slope 18 dB/oct · boost +6.0 dB) is in the explanation document — [Slope](EXPLANATIONS.md#11-why-the-slope-limit-is-not-18-dboct) · [Boost](EXPLANATIONS.md#12-why-the-boost-limit-is-62-db-and-above-10-khz-it-is-an-average).
    **The Improve method of Suggest correction…** lowers the excess to +6.0.
  - **A steep flank is fixed by the Improve method**. It brings the flank into the limit by lowering the Q of (widening) or reducing the gain of the one boost band that creates that flank, and picks whichever of the two
    changes the EQ curve less. When only the slope is exceeded, the first line of the warning is "탐지기가 가파른 부스트를 찾았습니다 — '보정 제안…' 의 '개선' 방법이 …" (The detector found a steep boost — the 'Improve' method of 'Suggest correction…' …). A flank that Ostrum created is
    not fixed with EQ, and the reason is left in one line.
  - **Suggest correction…** (enabled only when the correction would change anything): choose between two methods — **Industry convention (업계 관례)** (only lower the Preamp: max gain + 0.2 dB, shape unchanged — if there is an excess boost or a steep flank
    this method is not used and the window opens on Improve) / **Improve (개선)** (fix only the EQ boost in the exceeded band and the band that creates the steep flank
    with the smallest change, plus the Preamp if needed). The chosen method is remembered. It shows a **table of the changing bands** (band · type · frequency · gain before → after · Q before → after), the final curve before (dotted) and after (solid) the correction,
    and the criteria and their source. When nothing changes, **Apply correction (보정 적용)** is disabled and it says "바뀌는 것이 없어 '보정 적용' 을 끕니다." (Nothing changes, so 'Apply correction' is turned off.) It goes to the engine only when you press **Apply correction**, and the window carries the warning "이 보정은 안전을 우선해 곡선을 깎습니다 — 원하시는 소리와 달라질 수 있습니다. 적용할지는 직접 정하세요." (This correction cuts the curve to put safety first — the sound may differ from what you want. Decide yourself whether to apply it.) (it is heard immediately like other edits, and save to keep it). If the engine does not accept it (out of range · no engine · rejected · read-back differs) it says "보정을 엔진에 보내지 못했습니다" (The correction could not be sent to the engine) and the reason is in the EQ status line —
    the correction is in the edit draft. **Undo correction (보정 되돌리기)** goes back one step. It does not change Ostrum · Crossfeed — what Ostrum exceeded alone remains as "Ostrum 탭에서 줄이세요" (Reduce it on the Ostrum tab).
  - **Prevent clipping — lower Preamp automatically (클리핑 막기 — Preamp 자동 낮춤)** (checkbox, off by default; it stays on for people who had allowed the old automatic correction): this is the only automatic part. When on, if the sum of the EQ, Ostrum and crossfeed would go over 0 dB, **only the Preamp** is lowered by the needed amount — no band is touched and the curve keeps its shape. The lowered value shows on the detector row as `Preamp −2.1 dB (자동)` (automatic).
    A correction that reshapes bands happens only when you press **Apply correction**; Auto fit results and values you edited by hand are never changed by it. The result inside the detector’s ⓘ says what changed from before → after, and **Undo correction** goes
    back one step. Ostrum's **Automatically whenever it changes** (recommended Headroom) is judged as if the share it is about to move had already been moved, so the same excess is not reduced twice.
  - It is a sum of steady-state small-signal magnitudes — Harmonics · Bass dynamics · limiter · modulator are left out. If the settings could not be read or the Ostrum curve is being queried, "탐지기: … 판정하지 않습니다" (Detector: … no judgment is made) appears.

Tabs under the graph: **Equalizer · Ostrum · Crossfeed**.

### 6.2 Equalizer

**A change is heard immediately, and it remains only when you save it**.

- Header: **Equalizer** ⓘ (press for this stage's explanation) · **EQ On** · **Presets ▾ (프리셋 ▾)** · **Revert to saved (저장본으로 되돌리기)** · **Reset (초기화)** · **Save (저장)** (⌘S). The former **[EQ | Auto EQ]** tab is gone —
  Auto EQ is the collapsible row right before the band columns (§6.5).
  - Sliders · dots in the graph · number fields · type · channel · on · Graphic 31 · Open EQ Preset… · Auto fit · Apply correction — whatever you change goes **immediately to the engine and is heard.**
    While you drag by hand it is sent **at most 20 times per second (every 50 ms)**, and when you release, the last value is sent once more (provisional figures).
  - **Save** (⌘S): writes the EQ you are hearing to the app settings so it is used at the next launch too. Nothing is written to the settings file before you save — when you launch the app again
    it starts with **the EQ you last saved**. A value in a range the app does not accept is not saved, and the reason is stated.
  - The line under the header: `✓ 저장됨 · 다음 실행에도 이 EQ 로 시작합니다` (✓ Saved · the next launch also starts with this EQ) / `● 저장 안 됨 — 저장(⌘S)해야 다음 실행에도 남습니다` (● Not saved — it remains for the next launch only if you save (⌘S)) (orange) /
    `저장한 EQ 가 없습니다 — 저장(⌘S)하면 다음 실행에도 남습니다` (There is no saved EQ — if you save (⌘S) it remains for the next launch) (never saved). At the end of the line, in gray, what the engine holds now
    (`엔진 설정과 일치` (matches the engine settings) · `편집 중 · 아직 적용하지 않음` (editing · not yet applied) and so on) is attached — if the engine turned the EQ off because of the rate, that sentence goes to the orange line directly under it. The statement that a changed sound is heard immediately is in one line under the band columns. The values of disabled bands are not counted as a difference (the engine does not design them, so the sound is the same).
  - **Revert to saved**: back to the EQ you last saved — the sound goes back immediately too. Enabled only when there is unsaved change. One step at a time is **⌘Z** ([§2.6](#26-handling-knobs--sliders--eq-points)).
  - **Presets ▾** (between EQ On and Revert to saved; if a preset is chosen, its name — after editing, `name · 수정됨` (name · modified)): keep an EQ under a name and choose it again.
    - The **five most recent** (in the order last chosen or saved) · when there are more than five, **All presets** (by name). Choosing one is **heard immediately and the next launch starts with that EQ**. The headphone and target that EQ was made for come into the Auto EQ row with it. A preset saved before this was recorded shows an empty Headphone / Target with `이 저장본에는 헤드폰 정보가 없습니다 — 고르고 저장하면 함께 기억합니다` (This saved copy has no headphone information — pick one and save, and it is remembered with it). After you edit it by hand the line becomes `● 저장 안 됨` (● Not saved), and to keep that, save (⌘S) — saving remembers the headphone and target shown in the row. With a preset chosen, Save (⌘S) also writes the EQ and the headphone · target **into that preset**; changing only the headphone · target turns Save on too.
    - **Save as… (다른 이름으로 저장…)**: when you enter a name (up to 40 characters), the EQ you are hearing is **saved (the same as ⌘S) and** kept under that name. If the same name exists, it asks whether to replace it.
      Save as does not touch the current preset. Up to 100 presets.
    - **Manage presets… (프리셋 관리…)**: rename · delete (delete asks once and cannot be undone).
    - **Revert to a previous save (이전 저장본으로 되돌리기)**: every time you save (⌘S), **the EQ that had been saved before it** is kept here (the latest 20, newest first). A line looks like
      `오늘 14:03 저장 · 밴드 10 · 최대 +4.0 dB` (Saved today 14:03 · 10 bands · max +4.0 dB) (for one that was a preset, its name). Choosing one is heard immediately and the next launch starts with that EQ (its headphone and target come into the Auto EQ row). Saving the same EQ again does not add to it.
      It differs from the header's **Revert to saved** (which discards what you changed after saving) — this one is "what was saved before".
  - **Reset**: sets all bands and the Preamp to **0 dB (flat)** — the band type · frequency · Q · channel · on stay as they are, so you can drag the same dots again. It is heard immediately, and to keep it, save.
    (The former Reset EQ — the button that returned the bands to their default positions — has been replaced by this.)
  - **When you quit the app**, if an unsaved EQ is being heard it asks once — Save and quit · Quit without saving · Cancel.
    When the app is ended from a terminal (`kill`, ⌃C) it does not ask — it quits without saving, and gives the default output back to the original device as ⌘Q does.
- Status text (the second line of the header): "엔진 설정과 일치" (matches the engine settings) / "편집 중 · 아직 적용하지 않음" (editing · not yet applied) (within the 50 ms in which the hand is ahead of the engine, or a value the engine did not accept) /
  "엔진 기본값 · 아직 적용하지 않음" (engine default · not yet applied) (the engine's default that has never been
  applied — ten bands at 1000 Hz · off) / "이 레이트(N kHz)에서 설계할 수 없어 EQ 를 끄고 재생 중 · …" (Playing with the EQ off because it cannot be designed at this rate (N kHz) · …) (the engine could not build the EQ at this rate when playback
  started and left it out, orange). In the status after sending, "들리는 중 · 밴드 N개 · 최대 부스트 +N dB(합성 응답) · 프리앰프 −N dB 권장" (Being heard · N bands · max boost +N dB (combined response) · recommended preamp −N dB), the
  boost is how far the EQ curve (Preamp removed) rises above 0 dB at most, and the recommendation is that value + AutoEq's 0.2 dB margin — the same calculation as the Preamp of an AutoEq file, and it
  is not applied. The orange line under it, "지금 잘리고 있음 · Preamp −N dB 권장" (Clipping now · Preamp −N dB recommended), is shown only while the output stage is clipping right now or
  the limiter is pressing down peaks (N is the same calculation as the headroom value of Clipping & Headroom). When Ostrum is on, this line recommends the
  **main gain** −N instead of the Preamp — the Preamp comes before Ostrum, so lowering by the same amount does not lower the peaks by N. The two lines occupy their space,
  so what is under them does not move even when the sentence changes.
- **Saved settings remain for the next launch**. The saved (⌘S) EQ (bands · Preamp · on) and the EQ Backend, and also Crossfeed and the saved (⌘S) Ostrum request, are stored in the
  app settings, and when you launch the app again they are sent again before the engine starts its first playback. If the engine rejects what was sent again, under the header
  "적용하지 못했습니다 — 저장한 EQ 를 다시 보내지 못했습니다 — …" (Could not apply — the saved EQ could not be sent again — …) appears and the engine is left at its defaults. If the saved copy is corrupted or is a
  version this app does not know, it is not read and the app says so (the original is kept separately).
  **An Ostrum request held back while the engine was stopped** ("재생을 시작하면 이 설정을 보냅니다" (These settings are sent when playback starts)) is also saved. If you quit and relaunch in that state, it
  sends that request again and says "지난번에 보류해 둔 Ostrum 요청을 리비전 N 으로 보냈습니다 — 첫 재생부터 적용됩니다" (The Ostrum request held last time was sent as revision N — it applies from the first playback). After that, if there is a request the engine answered
  (accepted · rejected), the held copy is deleted, and if it was rejected, the settings the engine last accepted remain.
- **An EQ dropped at one rate comes back at another rate**. If the engine could not build the EQ at that rate when playback started and left it out, the saved
  EQ is left as it is and is sent again before the first sound the next time playback starts at a **different rate**. If it restarts at the same rate it is not sent (it would be left out again) —
  the line under the header says which case it is.
- When the EQ is turned on or changed elsewhere (shortcuts · the control channel), this screen changes to that value. Turning the EQ on/off by shortcut · the Playback menu · the control channel follows
  the same rule as the EQ On switch — heard immediately and not written to the settings, so `● 저장 안 됨` (● Not saved) appears. Even when pressed while there are unsaved edits, those edits are not
  saved (before, a single key press silently saved those edits too).
- When the EQ is turned off or the boost is reduced, the EQ is removed with a 10 ms crossfade (for the FIR backend, after the new kernel is ready), and if the PCM headroom is **Auto**, the gain that had been lowered goes back
  up **after** the EQ has been fully removed — sounding slightly quieter for a moment right after turning it off (usually 0.1–0.3 seconds) and then getting louder is intended. Before, the gain went up first, and turning off an EQ with a large boost caused a loud blast · tearing
  sound.
- **Band columns**: the first is the **Preamp** column (a vertical slider · field, and the row names under it
  Ch · Gain dB · Freq Hz · Q), then one column per band — the **on box and number** (pressing selects it — the dot in the graph is selected together) · a **vertical gain slider** ·
  a one-field pop-up for the **type** (PK · LS · HS · LP · HP · BP · NO · AP · G — the menu is Peaking · Low Shelf · High Shelf · Low Pass · High Pass · Band Pass · Notch · All Pass · Gain) ·
  **channel** (L+R · L · R) · **Gain · Freq · Q fields** (the up/down arrows beside a field = one scroll step). The selected band's column is faintly filled. The slider · field · dot are the same value.
  - In the default window (920), 10 bands fit on one screen, and with more the columns **scroll horizontally** (the Preamp column stays). In the minimum window (720), 6 columns.
  - The fields are shown short (16000 Hz → `16.0k`, 1234.5 Hz → `1.23k`) — pressing a field shows the full number, and you may also write it with a k such as `2.9k`. Confirm with Return.
  - At the head of the columns: `Bands N/32` · **Open EQ Preset…** · **Graphic 31** (0 dB peaking filters at the 31 ISO 1/3-octave places — the dots and sliders become a 31-band graphic EQ, replacing Curve mode) ·
    **Add Band** (the columns scroll to the new band) · **Delete Band** (the selected band) · **Reset Band**. **At most 32 bands, processed in list order.**
- The gain slider and the Preamp · Gain · Freq · Q fields also change **when you hold the pointer over them, hold ⌘, and swipe up and down with two fingers** (the value moves in the visible precision — Gain · Preamp 0.1 dB · Freq 1 Hz · Q 0.01 —,
  and per 6 pt of trackpad Gain · Preamp 0.5 dB · Freq about 0.1 octave · Q about 4.7 %, with ⌥ at 1/10 of that speed — §2.2). A value changed by swiping is also heard immediately.
- **Clipping & Headroom** is under the band columns (whether the Auto EQ row is expanded or collapsed) — because raising bands is what creates clipping (§6.6).
- **EQ Backend** (under the Equalizer tab): which filter to apply the same EQ bands with — **Parametric (파라메트릭)** (biquad, default · zero latency · exact magnitude · minimum phase with the phase turning
  slightly near the bands · no pre-ringing) / **Minimum-phase FIR (최소위상 FIR)** (the same magnitude made with a long FIR as minimum phase — the phase shape is of the same kind as Parametric, latency about 46 ms @44.1 kHz) /
  **Linear-phase FIR (선형위상 FIR)** (delays all frequencies by the same time so the phase does not turn — the ringing is divided before and after the sound, the pre-ringing can spread up to half the kernel length (about 186 ms @44.1 kHz),
  latency about 232 ms @44.1 kHz · 213 ms @48 kHz · 192 ms @192 kHz, and since the delay is reserved when playback starts, it takes effect **from the next playback start**). The two FIRs follow the magnitude within the realization error, and
  "Running / Next Start", Realiser Latency · Taps · **Max Realisation Error** are shown. Which one sounds better has not been confirmed by listening.
  If you choose FIR during playback and change the EQ, the EQ is heard immediately with **the backend that is running now** (usually Parametric), and at the end of the status line
  "지금 들리는 것: 파라메트릭 · 최소위상 FIR: 다음 재생 시작부터" (Being heard now: Parametric · Minimum-phase FIR: from the next playback start) is attached. FIR runs from the next playback — even after that the header line is still
  "엔진 설정과 일치" (matches the engine settings).
  If playback starts with the FIR backend, the EQ applies **from the first sound** (the sound comes out later by the backend latency). When you change the backend or bands **during** playback,
  it switches over 10 ms after the new filter is ready, as it does now.
- **Linear Phase Length (선형위상 길이)** (under EQ Backend when it is Linear-phase FIR): the length of the linear-phase FIR — ×½ · latency first / **×1 · Standard (default)** /
  ×2 · accuracy recommended / ×4 · most accurate. At 44.1 · 48 kHz that is 8 192 · 16 384 · 32 768 · 65 536 taps, latency about 0.12 · 0.23 · 0.46 · 0.84 s.
  The longer it is, the smaller the bass realization error and the greater the latency (the pre-ringing is almost unchanged). Each line shows the cost measured at 44.1 kHz and the taps · latency at the current rate.
  **65 536 taps is the upper limit**, so ×4 at 96 kHz and ×2 · ×4 at 192 kHz are marked "상한에 걸림" (hits the limit). The chosen length applies **from the next playback start**. For music listening where latency does not matter,
  ×2 is recommended.

### 6.3 Ostrum

A psychoacoustic tone shaper. For how to handle knobs at a glance, see [§2.6](#26-handling-knobs--sliders--eq-points) — it also appears as a tip the first time you open it. Knobs turn by drawing a circle, or by holding the pointer over one, holding ⌘, and swiping with two fingers; Shift or ⌥ gives fine adjustment (for both dragging and scrolling); double-click · ⌥-click is the default value; pressing the number lets you type it in. **You may also drag straight up and down** (like an audio plug-in, up = increase, 140 pt = the full range) — dragging straight in the vertical strip at the center of the knob is a vertical drag,
and drawing a circle is rotation, decided by the first 6 pt of the drag so the two do not mix during it. Holding **Shift or ⌥ (Option)** gives fine adjustment at 1/10.
**A change is heard immediately — and remains only when you save it** (the same rule as EQ). Moving a knob · Mode · the on/off switch goes to the engine right away
(once per 50 ms while the hand moves, and the last value when you release). It remains for the next launch only when you **save (⌘S)**, and **Revert to saved** goes back to the last saved Ostrum
(the sound goes back immediately too). The line in the header says `✓ 저장됨` (✓ Saved) / `● 저장 안 됨 — 저장(⌘S)해야 …` (● Not saved — you must save (⌘S) to …) / `저장한 Ostrum 이 없습니다 …` (There is no saved Ostrum …).
Under the card only the single line `움직이면 바로 들리고, 남기려면 저장(⌘S)합니다.` (It is heard as soon as you move it; to keep it, save (⌘S).) remains, and how to handle knobs is in the tip shown the first time you open it · the header's ⓘ · Help › Show controls (도움말 › 조작법 보기). **The Apply to Engine button is gone.** A setting the engine rejects is not saved, and the reason is stated.
Header (top): the name · a single **Ostrum On** switch (merging the former checkbox + On/Off badge — hold the pointer over the switch for the engine's report) · **Revert to saved** · **Save**,
then one line of Mix guidance (when Mix is 0 · the **Start naturally (자연스럽게 시작)** button), then the panel-wide **Composite Response** graph (160 pt tall).
The controls under it are **one board** with no boxes — a thin top rule and the names (Mix · Bass · Presence · Width · Harmonics · Headroom · Output) divide the sections, and depending on the
window width several sections sit on one row, wrapping to the next row when narrow, with both ends of each row aligned to both ends of the graph. There are only two knob sizes (Mix is large and the others are the same),
and on one row the knob names · knob centers · menus (Presence Mode · Harmonics Curve) · values stand at the same height.
If the PCM headroom is **Auto**, when you turn Ostrum on or raise the boost **the gain goes down first, and Ostrum enters after the engine confirms the drop**
(before, the modulator input was clipped for up to 0.5 second after turning it on). For those tens of ms the old sound plays.
An Ostrum on/off sent from outside the panel (the shortcut "Toggle Ostrum (Ostrum 켜고 끄기)" · the control channel's `ostrum-enabled`) is, like the EQ keys, **only heard and not saved** — to keep it, save (⌘S) in the Ostrum header. Other Ostrum commands of the control channel (Presence · Mix …) are sent as before and saved. The panel draws following that request.
The top line of the panel is what the engine received — "적용됨 · 리비전 N" (Applied · revision N) / when the engine has no accepted request yet, "엔진이 받아들인 Ostrum 요청이 아직
없습니다 — 아래 값은 요청이고 소리에 적용되지 않았습니다" (The engine has not accepted an Ostrum request yet — the values here are a request and are not applied to the sound) / when it rejected, "엔진이 마지막 Ostrum 요청을 거부했습니다: …" (The engine rejected the last Ostrum request: …). The reason for a rejection appears under the
header's save status line (the "리비전 N 요청을 보냈습니다" (Sent the revision N request) for each movement is not shown). Each rejection has one sentence per reason and says what to change — if Mix is above 0 while Tune is neutral (0) it says `엔진이 거부했습니다 — Mix 가 0 보다 크면 Tune 이 1.1–22 kHz 안에 있어야 합니다 — Tune 을 정하거나 Mix 를 0 으로 내리세요. (코드 4)` (The engine rejected it — if Mix is above 0, Tune must be within 1.1–22 kHz — set Tune or bring Mix down to 0. (code 4)); putting Tune back to 0 while Mix is above 0 gets the same sentence (bring Mix to 0 first, then Tune to 0); a Tune outside the range, Drive, the Presence mode and the input rate each have their own sentence. When the engine gave no reason, it says `엔진이 이 설정을 받지 않았고 까닭을 알리지 않았습니다 — 마지막으로 받아들여진 설정이 계속 들립니다.` (The engine did not accept this setting and did not say why — the last accepted setting keeps playing.). No sentence is only a code number.

- **Presets**: the **Presets ▾** menu next to the switch in the header.
  - **Four recommended starting values** (the parentheses next to a name in the menu hold the three values that distinguish that preset, and pointing at an item shows its Harmonics state and Amount in a tooltip):

    | Preset | Sound | Compression | Mix | Tune | Presence | Width | Harmonics |
    |---|---|---|---|---|---|---|---|
    | **Natural (자연스럽게)** | 0.40 | 0.08 | 0.20 | 3.5 kHz | 0.10 | 0.7 dB | Off (when turned on, starts at 0.02) |
    | **Clear OST·Vocal (선명한 OST·보컬)** | 0.50 | 0.12 | 0.30 | 3.0 kHz | 0.20 | 1.2 dB | 0.04 |
    | **Bass-forward·Electronic (저음 중심·전자음악)** | 0.75 | 0.25 | 0.38 | 4.0 kHz | 0.12 | 1.0 dB | 0.05 |
    | **Night·Low fatigue (야간·피로 적게)** | 0.30 | 0.05 | 0.15 | 6.0 kHz | 0.05 | 0.4 dB | Off |

    All four have Presence Mode **Min Phase**, Output 0 dB, Split Bass off, and Topology Blend. Pressing one **sends all the knobs, including Mix, to those values and is heard
    immediately** — to keep it, save (⌘S). If the knobs currently equal one preset, a check is attached to its name, and moving even one knob removes the check.
    The two that turn Harmonics on (Clear OST·Vocal · Bass-forward·Electronic) also put in the **recommended Headroom** of that setting when pressed (the current values −2.9 · −2.7 dB).
    The two with Harmonics off have Headroom 0, and the amount raised is restored by the PCM headroom Auto (measured on a fake device −4.8 · −4.3 dB).
    When you turn on the Harmonics curve in **Natural**, the amount starts at 0.02 (turned on in other settings, 0.25).
    These values are **suggestions that have not yet been confirmed by listening**. The former Light · Medium · Strong are gone — a setting or my preset saved as one of them keeps its values as they were.
  - **My presets (내 프리셋)** — when you write a name (up to 40 characters) in **Save current settings as my preset… (지금 설정을 내 프리셋으로 저장…)**, it goes into the list (the latest save on top; with the same name, it is replaced with the new settings).
    Choosing one from the list makes those settings heard immediately (save with ⌘S). **Rename** · **Delete** (after asking) are in the same menu. Deleting does not change the sound you are hearing.
    It remains only in this Mac's app settings (the name · save time · knob values — no track · device information). EQ's named saves have the same form.
- **Mix** is the first and largest knob — because it is the one to raise first. If it is on and Mix is 0, under it
  `Mix 가 0 이라 그대로입니다 — ‘자연스럽게’ 로 시작해 보세요.` (Mix is 0, so it is unchanged — try starting with 'Natural'.) (when Tune is neutral, `Mix 0 · Tune 없음 — ‘자연스럽게’ 로 시작해 보세요.` (Mix 0 · no Tune — try starting with 'Natural'.)) and the
  **Start naturally** button appear. Pressing it puts in the recommended starting value **Natural** and is heard immediately. The app does not raise values on its own — the one who presses is you.
- **Bass**: Sound · Compression · Tune (0 = Neutral) · Neutral Tune · Split Bass · **Topology** — Blend (default) / **Manual [Experimental]**.
  The **ⓘ** beside Neutral Tune, Split Bass and Topology tells you when to use it, what you hear, and when you can leave it. When you choose Manual, the graph also draws the Manual curve.
- **Split Bass**: Bass works below 1.1 kHz. Off, all of it is one path, so the boost and the Compression are one each. On, it is split into below 120 Hz (Soft) and 120 Hz–1.1 kHz (Tight), each with its own boost and Compression,
  and Sound sets the balance between the two. **When to turn it on**: you use Compression and are bothered that a loud deep bass note also presses the bass above it — on, the two bands do not press each other.
  Whether it sounds better has not been checked by listening. **When you can leave it off**: at Mix 0 nothing changes. It is off by default, and all four recommended starting points have it off. Sound, Compression and Mix keep their values either way.
- **Neutral Tune** means Tune is not used. Tune is the reference frequency from which Presence lifts the highs; Neutral Tune leaves it unset, so Bass and Presence are out and only Width, Harmonics and Output are used.
  **When to turn it on**: you want only Width or Harmonics, not Bass or Presence. At Mix 0 the Bass and Presence stages let the sound pass as it is. **When you can leave it off**: when you use Bass or Presence —
  to raise Mix, Tune must be set within 1.1–22 kHz, and with Presence Off the Tune value is not heard and only has to be in range. The state you start in, untouched, is already Neutral.
  The engine takes Tune 0 only with Mix 0 and Presence off, so the moment you check it the app sets Mix and Presence that way and tells you in one line what it changed. Unchecking it puts back the values from before (Tune · Mix · Presence). It is an unsaved edit, so save (⌘S) to keep it.
- **Blend and Manual**: Blend is the default and the sound so far. Manual is an experiment — choose it when you want to try a structure that leaves the original bass untouched at the centre of Sound. Whether to make it the default is decided after listening.
  The graph draws the response the engine computes for that structure, so the same knob values give different curves. **Sound**: in Blend the weight moves from Soft to Tight and, with Mix up, the bass is lifted at any position (6 dB for Soft and 3 dB for Tight at the ends).
  In Manual the centre (0.5) is the original bass (no change); lowering toward 0 grows Soft and raising toward 1 grows Tight, up to the end values. **Compression**: Blend presses the whole lifted bass, so with loud sound it can end below the original bass (measured on synthetic signals, not by listening);
  Manual presses only the part that was added, so it does not go below the original. **Presence**: Blend lifts by Intensity times Mix; in Manual Intensity only puts Presence in or out (0 is out, above 0 is in) and Mix alone sets the amount.
- **The Tune knob has a logarithmic scale** — the same angle per octave (about 62.5°), so 1.1–3 kHz is about 1/3 of the arc. 3 kHz is at half past ten o'clock, and 10 kHz is a little past the two o'clock direction.
  The low Hz is on the left, the same direction as the other knobs. Turning · vertical dragging · scrolling · ⌥/Shift fine adjustment all move by angle, so the Hz of one step is larger on the high side.
  Type the exact value by pressing the number. The Hz sent is the same, so the sound is unchanged.
- **Mix is the overall amount**: by default it is Mix 0 · Tune neutral, so raising the Bass · Presence knobs does not change the sound. Then, beside the knobs an orange line
  `Mix 가 0 이라 Bass · Presence 는 들리지 않습니다 — Mix 를 올려야 들립니다. 그 전에 Tune 을 1.1–22 kHz 안으로 정하세요.` (Mix is 0, so Bass · Presence are not heard — you must raise Mix for them to be heard. Before that, set Tune within 1.1–22 kHz.) appears.
  If you raise Mix with Tune neutral, `Mix 가 0 보다 크면 Tune 이 1.1–22 kHz 안에 있어야 합니다 — Tune 을 정하거나 Mix 를 0 으로 내리세요.` (If Mix is above 0, Tune must be within 1.1–22 kHz — set Tune or bring Mix down to 0.) appears.
  The sound is unchanged; only the sentence is added.
- **Presence**: Intensity · Mode (the knob and the mode side by side in one card) — Off · Analog · Min Phase · Linear Phase. **Linear Phase** is enabled only when the engine can reserve the delay at start —
  if you choose it during playback, "next playback" or **Restart Now** (the sound is cut briefly, and the length of the cut is measured and written).
- **Width**: the gain of the left-right difference (not a treble band control).
- **Harmonics** (Curve (Off / 2nd·3rd order poly23-v1) · Low Pass · DC Blocker · Amount) and the two cards **Headroom · Output**. When a **recommended Headroom** appears,
  move Headroom yourself or press **Set Headroom to the recommended value (권장값으로 Headroom 맞추기)** (pressing moves the knob and is heard immediately — save to keep it).
  Under the button, when you turn on the **Automatically whenever it changes** checkbox (off by default — the same component as Auto fit's "자동 조정 허락" (allow automatic adjustment)),
  the Headroom knob follows whenever the recommended value changes (the visible knob moves and is heard immediately · save to keep it). The setting you turned on is remembered for the next launch too.
  The recommended value is the curve share **plus Ostrum's own boost** — the amount that Bass · Presence · Width raise before Harmonics (for example, with a strong setting of +11.4 dB,
  −15.5 dB instead of −4.1 at Amount 1). The line states the two shares and their frequencies. If the boost is not yet known, only the curve share is shown and the button is locked. Headroom · Output is a flat gain that lowers the whole curve by that amount, so it is drawn without in the Response graph and the line under the graph states the values (§6.1). Low Pass 40 kHz · DC Blocker 5 Hz · Amount 0.25 when turned on are **provisional values** (not confirmed by listening).
- The Composite Response (small-signal magnitude) graph (one panel-wide row under the header): M (Mid, center · solid line) · S (Side, left-right difference · dotted line), with how to read it in the ⓘ.
  Headroom · Output are drawn without, like the Response graph — that value ("그래프는 모양 비교를 위해 Ostrum Headroom(-6.0 dB) · Output(-3.0 dB)를 빼고
  그립니다 …" (The graph is drawn without Ostrum Headroom (-6.0 dB) · Output (-3.0 dB) for shape comparison …)) and the explanation of the curve appear when you hold the pointer over the graph. The same line is also under the Response graph.
  The curve color is always Ostrum purple (before, it turned gray). **While Bass compression is pressing down**, a faint purple hatched fill appears
  under the M line — the fill's width is the band in which the compression acts, its thickness is the amount by which the sound is reduced by that compression, and `압축 중 −x dB` (Compressing −x dB) (the place reduced most)
  appears over the graph. The thickness is the difference from the curve the engine recalculated with the compression amount put in, so it includes the share of original sound mixed in by Mix — at Mix 0.5, even when the compressor presses
  3 dB the sound is reduced about 1.8 dB and the fill is that much too. The figure is the moment of deepest pressing within the last 0.1 second. When it is not pressing, there is
  no fill. In the moment while you turn a knob that the engine receives the new setting, the curve stays as it is, and if it is **not applied for more than 1 second** the two lines become sparse dotted lines
  and `적용 대기` (Waiting to apply) appears. The Ostrum · EQ + Ostrum lines of the Response graph are the same (the `압축 중` (Compressing) entry at the end of the legend).
- **LC-EQ** is in the engine but has no knob in this panel — the app returns the value the engine holds as it is, and since there is no way to change that value inside the app, it is always off.
  Drive · level matching also have no on-screen control (the engine rejects Drive if it is not 0).
- For a source outside the supported rates, Ostrum reports that it is undefined.
- Linear phase is **one Mode picker of Presence**. The **Presence Linear Phase** switch that used to be separately under the panel was a placeholder that was always rejected with "아직 엔진에 연결되지 않은
  기능입니다" (This feature is not yet connected to the engine), so it was removed. The empty `Custom` menu in the DSP header ("체인 프리셋 · 준비 중" (Chain presets · coming soon)) was also removed.

### 6.4 Crossfeed

- A **Turn crossfeed on (크로스피드 켜기)** switch and two knobs. **Amount / Feed (양)** is how much quieter the copy sent to the opposite ear is (−15.0 … −1.0 dB) — the nearer −1.0 dB, the more is mixed in.
  **Frequency / Cutoff (주파수)** is up to what pitch that copy is mixed (300 – 2,000 Hz) — the lower it is, the more only low sounds are mixed. You can press the number under a knob to type a value;
  double-click returns to the Medium value.
- Under the switch, **Light · Medium · Strong (가볍게 · 보통 · 진하게)** are default presets in order of how much is mixed (650 Hz · −9.5 dB, 700 Hz · −6.0 dB, 700 Hz · −4.5 dB — the three values published by the crossfeed
  library bs2b). Pressing one moves the two knobs to that value and turns crossfeed on. If the current values equal a preset, that button shows as pressed;
  when you move a knob, the line below changes to **Custom (사용자 지정)**. When it is off, the knobs dim and remember the values, and turning it on returns to them.
- The **My settings (내 설정)** menu saves the two current values under a name (up to twenty, names up to 40 characters; the same name asks whether to replace), loads them and deletes them. They stay after a restart.
  The names and values of the default presets are not saved separately.
- The **ⓘ** beside the line under the knobs is the adjustment guide — what each knob changes, and which way to turn when the sound feels trapped inside the head or the left and right feel too narrow.
- The two numbers under the knobs are the **low-band side signal** (how much left-right difference remains in the bass) and the **interaural time difference**. A note line appears at values where the time difference exceeds the limit of a real head
  (about 0.66 ms; a corner where a low frequency and weak mixing are chosen together) — it does not block.
- Turning on crossfeed together with Ostrum's Width shows a "width is being adjusted in two places" line. Both touch the left-right difference, so they partly cancel each other in the same band — the **ⓘ** at its end explains.
- If what you chose is not confirmed by the engine (the request and the engine's report differ), it says so.
- A small M/S window (Mid · Side): the center (L+R) stays at 0.00 dB and only the left-right difference (L−R) changes — that is why it is not included in the main graph.
  It is shown **only during playback** (the engine calculates it at the input rate). Even when stopped you can choose with the buttons.

### 6.5 Headphone ▾ · Target ▾ (the Auto EQ row of Equalizer) · Advanced — files · treble · Generative AI (collapsible)

Inside Equalizer, directly in front of the band columns, there is one **Auto EQ row** (not split into a tab · a separate window, because auto fit and hand editing are the same band columns).
- **When collapsed**: one line `Auto EQ   내 헤드폰 → 목표 · 밴드 10` (Auto EQ   My headphone → target · 10 bands) (within 40 characters — a long name is shortened in the middle, and if the strength is not 100 % `· 강도 70 %` (· strength 70 %)) and
  **Auto fit** at the end of the row. If there is no headphone · target, `헤드폰과 목표를 고르면 맞춥니다` (Choose a headphone and a target and it fits). One measurer-notice line is shown under it even when collapsed.
- **Pressing anywhere on the row** expands and collapses it. If there is no headphone or target yet, it is **expanded from the start**. If both exist it stays as you last left it within the app,
  and when you launch the app anew it starts collapsed.
- **Auto fit** is only one, at the end of this row — the same place when expanded. It is a blue (accent) button only when the headphone · target · number of bands · strength differ from the last fit (or when you have not fitted yet),
  and when the same it is a normal button.

When expanded, from the top come **Headphone ▾** · **Target ▾** · **Bands** · **Strength**, one status line, and two collapsible sections (**What auto fit did (자동 맞춤이 한 일)** · **Advanced — files · treble · Generative AI**).
**We did not include the condition grid (Bass/Treble Boost · Max Gain · Slope and so on)** — we judged it not to be needed.

- **Headphone ▾** (my headphone): when expanded, **My headphone favorites (내 헤드폰 즐겨찾기)** are shown at once in several rows (name · measurement site), and choosing one fetches and uses that measurement.
  Under them, **Search headphones… (헤드폰 검색…)** (the search window) · **Open measurement file… (측정 파일 열기…)** (opens the advanced collapsible). The **☆** beside the menu adds or removes the current headphone from my headphone favorites.
  When you change the headphone, the current target follows — if the target is a headphone, it stays; if it is a measurer's target, the same kind from the new measurer; if none, the list's default selection (DF t).
  Importing does not change the EQ (it changes when you press Auto fit).
- **Target ▾** (target): at the top the **target curves (타깃 곡선)** (the current headphone measurer's DF · DF t · Harman …, those that do not fit dimmed), under them the **target headphone favorites (목표 헤드폰 즐겨찾기)**,
  and under them **Search headphones…** · **Open target file… (타깃 파일 열기…)**. The **☆** beside it adds or removes the current target headphone from the target headphone favorites.
- **Favorites are two lists** — my headphone favorites and target headphone favorites are saved separately.
  If you open the search window from Headphone ▾ the star goes to my headphone list, and from Target ▾ to the target headphone list.
  Only the address and name are written to `HeadphoneFavorites-v2.json` in the app data folder. The earlier version's `HeadphoneFavorites-v1.json` is not deleted, and
  when v2 does not exist its entries are read as **both lists** (v2 is created when you first press a star).
- **A target headphone measured on a different rig**: it is not blocked. If the rig families (5128 · 711) of my headphone and the target headphone differ, the status line says so, and
  a **Rig difference correction (측정기 차이 보정)** checkbox appears (on by default). When on, it shifts the target toward my rig by a curve built from the differences
  of paired measurements — the same headphone measured on both rigs (it is in the app, one for headphones and one for earphones); nothing is downloaded. Only when it is not known
  whether it is a headphone or an earphone does it shift by the difference of the two measurers' DF curves (the two DF files are fetched from each measurer's server), and if either
  measurer has no DF it is used without correction and that is stated. When off, the target curve is used as measured. A **target curve** such as a preference target · a measurer's target is also moved by the same curve when its name states the other rig (for example a "711 …" target on a 5128 headphone). A **DF target is not moved but swapped**: a DF is what the two rigs measure differently in a diffuse field, a different quantity from the difference of a headphone worn on them, so it is replaced by the DF curve the same measurer published for my rig (pairing line "측정기가 달라 내 측정기의 DF 로 바꿨습니다" (The rigs differ, so it was swapped for my rig's DF); a tilted DF keeps its tilt). If that measurer has no DF for my rig it is moved by the curve above — with the checkbox off it is fitted as it is and one line "다른 측정기용 타깃이라 차이가 날 수 있습니다" (This is a target for a different rig, so there may be differences) appears. If you correct the rig family in the search window, it leaves the target in use as it is (a moved target stops) and shows a button that changes it to the same kind of the new family.
- **Sites that do not state their rig**: squig.link headphone DBs whose measurer did not record the rig are handled by the **site table** built into the app. It holds, per site,
  the rig family estimated ahead of time from the average of up to 60 of its headphone curves, and that site's headphones are corrected by that probability without asking (pairing line
  "측정기가 달라 보정해 맞춥니다" (The rigs differ, so it fits with a correction), the estimated probability in the ⓘ). The table vouches only for the headphones that were in the list when it was
  made — a headphone added later may be on a rig the measurer changed to, so it is not estimated until the next table. One measurer's own target curves and other headphones are taken as one rig and fitted as they are.
- **Rig cannot be estimated (측정기 추정 불가)**: a target whose rig is neither stated nor in the site table, so that its relation to my headphone's rig cannot be told, is **hidden from the target lists** —
  earphone DBs (the site table covers headphones only), headphones added after the table was made, and sites that state a rig other than 711 · 5128 (miniDSP EARS and the like).
  "측정기 추정 불가로 숨긴 목표 N개" (N targets hidden because the rig cannot be estimated) appears at the end of the list, and a press on a favorite or on **Use as target** in the search that finds it out first does not apply it, with that reason.
  If my headphone is from such a site, only that measurer's targets can be chosen. Telling the rig with **Fix rig family (측정기 계열 고치기)** in the search window shows them again.
- **Pairing line**: when you choose a target, one gray line and an ⓘ say what its pairing is — "측정기를 몰라 보정 없이 맞춥니다" (The rig is unknown, so it fits without correction) · "측정기가 달라 보정해 맞춥니다" (The rigs differ, so it fits with a correction) ·
  "측정기가 달라 보정 없이 맞춥니다" (The rigs differ, so it fits without correction) · "같은 측정자 · 같은 측정기의 측정입니다" (It is a measurement by the same measurer · the same rig) · "측정자가 달라 결과가 조금 다를 수 있습니다" (The measurer differs, so the result may differ slightly) · "다른 측정기용 타깃이라 차이가 날 수 있습니다" (This is a target for a different rig, so there may be differences). If the target is of a different kind from my measurement (headphone ↔ earphone), instead of this line a yellow "이어폰용 타겟 — 헤드폰에는 맞지 않을 수 있습니다" (Earphone target — it may not suit headphones) ·
  "헤드폰용 타겟 — 이어폰에는 맞지 않을 수 있습니다" (Headphone target — it may not suit earphones) comes first. The detailed sentences are in the ⓘ.
- **Status line**: one of the reason the last attempt was not applied (orange) · the reason Auto fit cannot run · the fit result (the pairing explanation moved to the pairing line). It always holds two lines of height so what is under it does not move.
- **When the target did not change**: if a target pressed in the search window · a pick in **Target ▾** · **Open target…** cannot change the target (a fetch failure ·
  the squig.link connection is off and so on), "마지막 시도(목표로 · 이름)는 적용되지 않았습니다 — 까닭 지금 타겟은 그대로입니다." (The last attempt (Use as target · name) was not applied — reason. The current target is unchanged.) stays in orange in the status line.
  It stays even if you close the search window, and disappears when you fetch a new target or change the measurement.
  If the search window's **Get list (목록 받기)** · headphone fetch also fails (the squig.link connection is off and so on), "찾기 창의 마지막 시도(목록 받기)가 실패했습니다 — 까닭 지금 측정과
  타겟은 그대로입니다." (The search window's last attempt (Get list) failed — reason. The current measurement and target are unchanged.) stays in the same place, and disappears when the same fetch succeeds.
- **Target file type** is **the kind of the target file you open next (Open target…)** — changing it does not change the current target (that is written under the field).
  A target chosen from the list records its kind itself.

- **Search headphones…** (the search window): it fetches squig.link's measurement list as a whole and searches **on this Mac** (the search term is not sent out — the ⓘ beside the title).
  Opened from Headphone ▾, the headphone you press becomes my headphone; opened from Target ▾, it becomes the target. **A press picks it and closes the window** — there is no separate apply button.
  Picking does not change the sound; the EQ changes only when you press **Auto fit**.
  - The window, top to bottom: the headphone (or the target) in force **now** · the kind (headphone · in-ear·earbud) and the search field · the list line · one list.
  - The **now (지금)** line has the name, one line "measurer · rig", **Check on squig.link (squig.link 에서 확인)** (opens that headphone in the squig.link graph — where the rig was read is seen there too)
    and **Fix rig family (측정기 계열 고치기)** (5128 · 711 · unknown · as it was — written on this Mac only). The rig description · the calibration file · the file count and left-right difference · the clone notice
    are behind the ⓘ at the end of the "measurer · rig" line. When finding a target headphone, the current target's name · measurer · original rig (the family before correction) and the pairing line show.
  - **One list**: with the search field empty it shows the favorites (added with ☆); typing shows the matches in the same place. Each row has the name and "measurer · rig"
    (the rig read from a configuration already downloaded — if none was, the list's own mark or "unknown", and nothing extra is downloaded to show it).
  - Picking my headphone brings that measurer's default target (**DF t**). A measurer's target curves (DF · DF t · Harman …) are chosen in the workbench's **Target ▾** —
    per family in the order **DF · DF t · Harman OE · Harman IE**, the rest in the measurer's order. **DF t** adds −1 dB/oct to DF (0 at 632 Hz),
    and if the measurer has no tilted DF file ("… DF (-1dB tilt)") the app builds it from that DF. Auto fit does **not add** a slope to the target.
    To use the measurement with no target, **Target ▾ › No target (목표 없음)**.
  - If the rig family is unknown or the measurer's setting differs from the DB's label, that measurer's targets are applied **as measured, without correction** — a target whose name states another rig has nothing to be moved by and is hidden ("Rig cannot be estimated" above).
  - **Once the list is fetched, it is not fetched again for 30 days.** When the window opens with the list in the cache it is **shown at once without pressing anything** — nothing is sent.
    The first time, press **Get list (목록 받기)**. With the mouse over the count, "캐시: 3일 전 받음 · 26일 뒤 만료" (Cache: fetched 3 days ago · expires in 26 days) appears, and **Refresh (새로 받기)** in the ⋯ beside the count fetches again.
    While fetching you can search what arrived first. If a DB does not arrive within 30 seconds or cannot be fetched, one line "받지 못한 DB N곳" (N databases not fetched) and **Try again (다시 시도)** appear at the bottom of the window
    (hover the words to see which) — the list on screen stays. A DB whose list has vanished from squig.link is left out without being counted, and with the mouse over the count it appears in "Sites not read (읽지 않는 사이트)".
  - **Favorites (stars)**: press the star in front of a row — it goes into the list of the menu that opened the window (my headphone · target headphone) and shows in Headphone ▾ · Target ▾ at once.
    Only the address and name are written to `HeadphoneFavorites-v2.json` in this Mac's app data folder (curves are fetched when you press). A headphone that disappeared from the list is kept and marked "목록에서 찾지 못함" (Not found in the list).
  - **Another headphone as the target**: in the window opened from Target ▾, only targets of the **same kind** as my measurement (headphone · in-ear·earbud) show first; the other kinds appear
    with **Show other kinds (다른 종류 보기)** under the list. Choosing another kind is not blocked; one line like "이어폰용 타겟 — 헤드폰에는 맞지 않을 수 있습니다" (Earphone target — it may not suit headphones) shows.
    A press fetches that headphone's measurement at that moment and uses it as the target. A different rig is corrected; a target whose rig relation cannot be told is hidden or not applied
    (the "target headphone measured on a different rig" · "Rig cannot be estimated" above). Pressing another target while one is still coming in keeps only the last press.
    In either case the gray pairing line and ⓘ say what was done. Only the frequency response measured on the rig is fitted; wearing state · ear shape · distortion are not.
  - **Number of measurement files · left-right difference**: the ⓘ of the "measurer · rig" line has a line like "측정 파일 3/4개(L 2 · R 1) · 좌우 차 RMS 0.8 dB, 최대 2.4 dB(20 Hz–10 kHz)" (Measurement files 3/4 (L 2 · R 1) · left-right difference RMS 0.8 dB, max 2.4 dB (20 Hz–10 kHz)).
    It is a fact about how many measurements were averaged and how much the left and right differ, not a judgment of good or bad.
- Opening directly ("Open from file" in the collapsible **Advanced — files · treble · Generative AI**): Headphone (name) · Rig (rig) · **Open measurement…**,
  Target file type (Family target DF · preference / Headphone target / Other headphone — the kind of the file to open) · "Open target (same rig family)…",
  and rarely used fields (Measurer · Rig ID · Target rig · Target measurer · Target rig ID).
  The file is a 2-column Hz·dB text or metadata JSON. **The level is as in the file, and no normalization or tilt is added.**
  A measurement opened from a file can also choose a headphone favorited in the search window as the target.

### 6.6 Bands · Strength · Auto fit (the Auto EQ row of Equalizer) · What auto fit did (collapsible)

Choose **Bands** (number of bands) · **Strength** (correction strength) and press **Auto fit** at the end of the Auto EQ row — pressing once finishes it. The sentences · figures of the fitted result (Fit Result) · the explanation of strength are in
the collapsible **What auto fit did** (collapsed normally, opened by pressing anywhere on its box row), and **Treble (Auto fit)** · Refine with generative AI (생성형 AI로 다듬기) are in the collapsible **Advanced — files · treble · Generative AI**.
The former **Auto fit & Refinement** collapsible (the second Filters · Fit button) has been removed.
**Clipping & Headroom** is outside the collapsibles, always visible under the band columns (whether the Auto EQ row is expanded or collapsed).

- **Bands**: the commonly used **8 · 10 · 12 · 16** are chosen with one press, and other numbers are dragged with the slider beside them (1–32). 10 is AutoEq's default.
  If a narrow bump (——\/——) remains at 4–8 kHz after fitting, raise to 12–16 and Auto fit again (an example measured on one headphone: going from 10 → 16 reduced the
  maximum 2–6 kHz fit error from 2.0 → 0.57 dB).
- **What Auto fit tries one more time**: when the fit is finished, it moves the least-used filter to the place with the largest remaining error and fits again (at most
  three times). If **any one** of the Fit Result figures (Mean · Max Error, Narrow Filters, Max Boost) and the largest error at 2–8 kHz gets worse, **that attempt is
  discarded** — so fitting again with the same measurement · target may differ from the previous version, and when it differs, it is the side with reduced error. The EQ you saved does not change.
- **When Ostrum is on**, a line appears under Auto fit — Auto fit fits **only the EQ**, and the graph's **After correction** line has Ostrum added as well,
  so it may look off the target (for example, the bass looking swollen after fitting with Harman 2024 β was Ostrum).
- **Auto fit (자동 맞춤)**: choose Bands and press **Auto fit**. The engine fits from the measurement and the target (corrected, if it is a target headphone on another rig), and the result goes into the band columns and
  **is heard immediately** — save (⌘S) to keep it. Fit Result: Mean Error · Max Error, Narrow Filters, Max Boost, Recommended Preamp, Iterations.
  **What auto fit did** (collapsible) — after fitting there is one sentence per band. Example: "3 kHz 부근 4.0 dB 줄임 — 중고역(upper mids) · 날카로움(harshness)·또렷함(presence) 쪽 ·
  폭 약 1.0 옥타브(Q 1.41)" (Reduced 4.0 dB near 3 kHz — upper mids · toward harshness · presence · width about 1.0 octave (Q 1.41)). For a shelf, "105 Hz 아래 전체 …(로우셸프, low shelf)" (Everything below 105 Hz … (low shelf)), and the last line is the Preamp. They are sentences made by rules (not AI) and are not a judgment of the tendency of what is heard.
  The region names follow mixing convention and the boundary Hz are approximate. The size of a single band is not judged — AutoEq's +6 dB is the limit of the correction curve before fitting, and the fit uses one band up to ±20 dB (when 100 real headphones are
  fitted with 10 · 16 · 32 filters, 53 · 46 · 33 of them have a band exceeding +6). Whether the combined curve is excessive is looked at by the excessive-settings detector. One guidance line under the sentences says so.
  If you edit a band after fitting, "맞춘 뒤 밴드를 고쳤습니다" (A band was edited after fitting) is attached — the sentences describe the bands right after fitting. The explanation changes nothing.
- **Strength (보정 강도)** (correction strength, 0–100 %, default 100 % — one line under Bands inside the Auto EQ row, explained inside "What auto fit did"): reduces the auto fit result by a ratio — it multiplies each band's gain by the ratio
  (frequency · Q unchanged) and recalculates the Preamp (0.2 dB under the maximum of the combined response). **100 % is the fit result as it is** (the same sound as until now) and
  0 % is no correction. Moving it puts the last fit back into the editor at that strength — if you edited a band after fitting, it does not overwrite your edit and is used from the next fit.
  The strength remains for the next launch. Moving the strength is also heard immediately (save with ⌘S), and since the boost shrinks by the same ratio the excessive-settings warning shrinks too.
  At the end of the line under the strength, "(적용됨)" (applied) if the editor equals the engine, otherwise "(편집기 · 아직 적용 전)" (editor · not yet applied) (within the 50 ms in which the hand is ahead).
- **Clipping & Headroom** (under the band columns, not collapsible): whether this playback's output stage is clipping, Limiter (Limiter Threshold · Engaged · Max Reduction), the **Apply Headroom N dB**
  suggestion button (lowers the PCM headroom and switches it to **Manual** — Input/Output (입출력) › ③ "자동으로 되돌리기" (Return to automatic) brings it back), **Turn Limiter On / Off** (off by default).
  If the PCM headroom is Auto, the amount raised by EQ · Ostrum · Crossfeed has already been lowered, so what makes the counter here stand is a peak larger than that (a large inter-sample peak and so on). The two buttons are on the **Clipping & Headroom** title row. The sentence row always reserves as much room as it takes at its fullest,
  so the fields under it do not move when clipping occurs or disappears (normally an empty space is visible).
- **Refine with generative AI (생성형 AI로 다듬기)**: three steps. **1 · Take your settings out (내 설정 꺼내기)** — save the measurement · target · current filters with **Export to file… (파일로 내보내기…)**, or **Copy text for the AI (AI에 줄 글 복사)**.
  **2 · Refine in the generative AI you use (쓰는 생성형 AI 에서 다듬기)** — give that file or text to ChatGPT · Claude and so on and ask it to refine the EQ (outside the app; the app sends nothing).
  **3 · Bring the result back (다듬은 결과 다시 들여오기)** — **Open result file… (결과 파일 열기…)**, or paste the AI's reply and press **Import pasted reply (붙여 넣은 답 가져오기)**. Opening a file makes the app show the values it measured
  (number of filters · narrow filters · max boost · target error) and **Import to editor (편집기로 가져오기)**. An error the AI wrote is shown separately as "검증 안 됨" (not verified).
  - **Text for the AI**: write one line (for example "치찰음이 거슬린다" (sibilance bothers me)) and **Copy text for the AI** → paste it yourself into the generative AI you use.
    The prompt contains the headphone name · rig family · target name, the current band table (type · frequency · gain · Q) and the Preamp, the difference between measurement and target (octave · 1/3-octave averages with 1 kHz set to 0 dB,
    the difference remaining after adding the current EQ), the one line you wrote, the limits to keep (number of filters · range · combined boost +6 dB · a flank above 0 dB not steeper than a PK at the same place (Q 6 · +6 dB) (the same as the detector's slope rule) ·
    Preamp margin 0.2 dB), and the format to be returned. How the app calculates inside is not included. You must open the measurement and target first.
  - Paste the LLM's reply into the field and press **Import pasted reply** → the `Preamp:` · `Filter N:` lines of the last code block are put into the band columns by the same
    reading as **Open EQ Preset…** — **it is heard immediately**, and save (⌘S) to keep it. If there is a line that cannot be read, what is missing is written.

### 6.7 The A/B button's panel — A/B · ABX · Auto Bypass · Loop · Level-matched Comparison (음량 맞춤)

Pressing the small **A/B** button at the end of the header expands it directly under the header (before, it was a bar at the very top of the page and a collapsible row).
Because it is in the page and not in a window, **you can keep it open and touch the EQ under it.** Pressing once more collapses it. The features and button names are as they were.
The details of slot values · Level Match · ABX · Auto Bypass · Loop **scroll separately** inside the panel (220 pt tall — so that expanding it does not push the graph out of the first view).

- **Manual A/B**: Save Current to A · Save Current to B → **Start A/B** → Request Slot A/B (gapless switching) → End Comparison.
  **Level Match** (음량 맞춤) is on by default — it lowers the louder side to the same loudness (BS.1770 K-weighted integrated), and Match Gain is always shown.
  Manual A/B does not end when the track ends but ends **only when the user ends it**, and when it ends you stay on the side you were listening to.
  If the engine refuses the comparison, **the reason is shown with it** in that place — the engine's A/B refusal reason (the limiters of the two slots differ and so on) or the engine's answer and code (for example, `엔진이 값이나
  지금 상태를 받지 않음 · 코드 3` (The engine does not accept the value or the current state · code 3)).
  **Even when the EQ Backend is Minimum-phase or Linear-phase FIR**, A/B · ABX · Auto Bypass start, and the two slots are heard with the EQ each saved. The two slots must be saved **with the same EQ backend family** — if you compare a slot saved in Parametric in FIR playback (or the reverse)
  it is refused with `슬롯 A 를 저장할 때의 EQ 백엔드가 이번 재생과 다릅니다 … 지금 백엔드에서 슬롯 A 를 다시 저장하세요.` (The EQ backend when slot A was saved differs from this playback … save slot A again with the current backend.) and playback continues as it was.
- **Auto Bypass** (the Ostrum-on side ↔ the off side, **Start Auto Bypass**): Switch Interval · First Comparison · Measurement Time. The track keeps flowing and the sides alternate at every interval.
  Even if you end while listening to the original, it returns to the processed side (Ostrum on). It does not start if Ostrum is off.
- **Loop Comparison** (compare using the section you heard a moment ago, **Start Loop Comparison**): rewinds Look-back N seconds and, each lap (Lap), alternates processed ↔ original. **Only in file playback**, and it cannot start if the next file is in
  the queue.
- **ABX**: within a comparison session. The number of trials (Trials) is decided before **Start ABX** (default 16), and until the end the number of correct answers and the side being heard are hidden. X is A / X is B /
  Stop (no verdict). Recent Runs on This Mac (이 기기에 기록된 최근 실행) remain under it.


## 7. I/O · Diagnostics Page

### 7.1 Independent output control · Output mode

- Engine on/off (normally controlled with the play button).
- **Output mode (출력 방식)** (at the very top of the page, always visible): from the first launch you pick one of three — **PCM Direct** / **DSD (DoP)** / **PCM 352.8 kHz**.
  A line under your choice says what the sound passes through. For PCM 352.8 kHz (and for local files in PCM Direct) you pick the **bit depth** (24 · 16-bit) and the
  **dither** below it. Previously you picked "Fidenne engine / PCM Direct" and then chose DoP or PCM again in the card below — that setting had no saved value,
  so there is nothing to migrate. **The output mode you pick is kept for the next launch** — except that DSD (DoP) and PCM 352.8 kHz
  are restored only if there is a record that the engine opened that format on the chosen DAC (the ✓ in the §7.2 table, with the DSD rate to start at and the bit depth as they were). If there is no record, the record is a rejection, or
  no DAC is chosen, it **starts as PCM Direct**, and the header of the DAC format check card shows one line, `PCM Direct 로 시작합니다 — …` ("Starting as PCM Direct — …"). Your choice
  is not erased, so turning it on again with a verified DAC brings it back. Launching the app does not by itself start the engine (as before). **If an update removed a saved setting or changed its meaning** (a retired filter · a value that does not exist in this version), only that field is reset to the recommended value (the app default; for a retired filter, the closest filter), and the window header shows one line, `업데이트로 ○○가 바뀌어 권장값으로 초기화했어요` ("An update changed ○○, so it was reset to the recommended value"), with "before → now (reason)" for each value. **Go to settings (설정하러 가기)** scrolls to that card on the I/O page and briefly highlights its border; the notice stays for later launches until you press **Close (닫기)**. Values that can still be used are kept as they are, with no notice. PCM Direct goes playback app → macOS PCM → the selected DAC, and it
  skips the engine (EQ · Ostrum · Crossfeed · filter · DSD conversion), so **DSD headroom is not applied** — check the DAC volume before switching. Choosing the output DAC · refreshing · connecting / reconnecting the DAC.
- **PCM Direct** — Fidenne does not process the sound. It goes player app → macOS → DAC. The sample rate is not matched track by track (because the sound does not pass through Fidenne, it cannot change the output rate to the track's (input) rate): when the DAC's rate and the track's differ, macOS converts. The DAC's rate is set once at start (44.1 kHz for Spotify; the track's rate or 44.1 kHz when the DAC sits at a rate that is not ordinary PCM, such as DSD or 352.8 kHz).
  **DSD · PCM 352.8 kHz** — with EQ · Ostrum · Crossfeed off, nothing changes the tone, but the conversion each format needs (upsampling filter · DSD modulator · dither · headroom) is applied, and the chosen filter and modulator can change the character of the sound.
- If the DAC is currently at a normal PCM rate (44.1–192 kHz), PCM Direct uses that rate as it is; if the DAC is at a rate left behind by DSD or the engine's PCM output
  (352.8 kHz and so on), it changes to the playback app's rate — Apple Music uses the track's rate, Spotify uses 44.1 kHz. If the playback app's rate
  is unknown (a browser · the track rate cannot be read), it **sets 44.1 kHz** and writes the reason on one line under "DAC connected (DAC 연결됨)" on the PCM card — a track at a different
  rate is converted by macOS. **Spotify always switches the DAC to 44.1 kHz unless it is already 44.1 kHz** (even at a normal rate such as 48 kHz) — if it is already 44.1 kHz it is left alone, and if the change fails the red band shows `PCM 레이트 설정 실패 (CoreAudio …)` ("Failed to set PCM rate (CoreAudio …)").
  In every case it uses **only rates the DAC reports it accepts** — on a device that accepts only 48 kHz and not 44.1 kHz (an HDMI TV · some USB-C
  adapters), it either leaves the DAC's current rate as it is (when that is a normal rate) or sets 48 kHz, and writes under "DAC connected (DAC 연결됨)":
  `이 DAC는 재생 앱의 44.1 kHz를 받지 않아 48 kHz로 재생합니다. macOS가 변환합니다.` ("This DAC does not accept the playback app's 44.1 kHz, so it plays at 48 kHz. macOS converts.")
- Moving the same USB DAC to another port may change its device ID. After the engine stops, a unique match of USB manufacturer, model and serial number restores it as the saved output and carries its DoP confirmation.
  A model without a serial number is recognised only when there is one matching device. If there are multiple candidates or USB identity cannot be established, choose the output DAC yourself.
  Older settings learn USB identity when their saved device ID is actually listed. An unidentified look-alike may still be labelled `· 저장된 DAC와 같은 모델` ("same model as the saved DAC").
  USB identity is stored only in this Mac's settings. Format verification results are not copied to the new ID.
- In the output DAC list (including the list in the first-run guide), **devices that do not accept 352.8 kHz** (built-in speakers · AirPods · most dongles · monitors) get
  `· PCM Direct 만` ("· PCM Direct only") at the end of the name. On such a device only listening to Apple Music · Spotify in PCM Direct works; DSP such as EQ · Ostrum · Crossfeed
  and library playback do not (the engine runs only on DACs at 352.8 kHz or above, as it does now). If you turn on the engine with that device,
  play a library track, or press **Check all (모두 확인)**, one line appears: `이 장치는 352.8 kHz 를 받지 않아 DSP 와 보관함 재생을 쓸 수 없습니다. 외장 DAC 를 고르세요 - …` ("This device does not accept 352.8 kHz, so DSP and library playback are unavailable. Choose an external DAC - …"). A device that accepts 352.8 kHz but has no 2-channel format the engine uses, such as an 8- or 4-channel interface, gets a different reason (`… 2 채널(스테레오) 형식이 없어 …`).
  The label is only a notice; it does not stop you from choosing the device.

### 7.2 DAC format check (formerly "Engine output format")

- Choosing the format moved to **Output mode** in §7.1. PCM **dither**: Default (1st order at 24-bit · 2nd order at 16-bit) · Off (rounding only) · TPDF · No shaping ·
  TPDF + 1st/2nd/3rd-order shaping. Each choice states its trade-off.
- If the DAC does not accept the chosen PCM format, it **does not drop to another rate and does not start.**
- **One table**: for each of four formats (DSD128 · DSD256 DoP · PCM 24 · 16-bit), **Verified** (✓) · **Rejected by the engine** (⚠ + reason) · **Declared · not yet verified**
  (clock) · **Unknown**. The header reads `선언한 형식 N개 중 M개 확인됨` ("M of N declared formats verified"). The verification result is **remembered per DAC** — it stays even if you change the format or the device list
  changes (which happens at every tap start), and even if you relaunch the app. If the same DAC reports a different format table (it appears as a different device), only that DAC's memory is erased.
  The memory is stored in settings as `aural.output.verifiedFormats.v1` (only the DAC UID · format · verified/rejected · reason number).
- **Check all (모두 확인)**: pressed with playback stopped, it has the engine set and read back each declared format that has not been verified yet, in turn (the format you currently chose goes last),
  and then restores the original format — no sound goes out and playback does not start. The DAC may click while the format changes, or the display may change briefly.
  It cannot be pressed while playing, while the playback app is playing, while output is being prepared, or when the DAC is not in the list, and the reason appears on one line. While it runs, starting playback ·
  local-file playback are made to wait. When it finishes: `새로 확인 N개 · 거절 N개 · 답을 받지 못함 N개` ("N newly verified · N rejected · N no answer") — "no answer" means a failure for a reason that is not the format
  (input · another app), so it is not written into the table.
  After each format is verified, the engine is **returned to the stopped state** and it moves on to the next format — when it finishes the engine is always stopped, and settings · choosing the output DAC are
  released immediately (previously the engine stayed in the ready state after the first format, so the remaining formats became `답을 받지 못함` ("no answer"), and settings stayed locked until you pressed
  stop).
- **DoP row**: **Verified** in the table means macOS set that format and read it back; it does **not mean the DAC decodes DoP** —
  a DAC that cannot decode DoP plays DoP as loud noise. So **starting DoP with a DAC you have not used before asks once**: a window says
  `<DAC 이름>로 DSD(DoP)를 처음 보냅니다` ("Sending DSD (DoP) to <DAC name> for the first time") — **DoP를 받는 DAC · 시작** ("A DAC that accepts DoP · Start") (remembers it and starts) · **PCM 24-bit로 재생** ("Play as PCM 24-bit") (changes the engine output to PCM 24-bit and starts)
  · **Cancel (취소)**. The first time, lower the volume or take off your headphones, and check whether the DAC's display · indicator light shows DSD. The answer is remembered per DAC (in settings as
  `aural.output.dopConfirmedDevices.v1` — DAC UID only), and an output DAC that was already saved when this version was first opened is not asked (it has been sent DoP all along).
  If the same DAC reports a different format table, including after a port move, its confirmation is withdrawn and the next DoP start asks again.
  Returning to an earlier port after **Ask again** does not restore that confirmation.
  The line under the table reads `DoP: 이 DAC는 DoP를 받는다고 확인함` ("DoP: confirmed that this DAC accepts DoP") · **Ask again (다시 묻기)**, or `DoP: 확인 전 · 처음 DoP로 재생할 때 묻습니다` ("DoP: not yet confirmed · asks when you first play with DoP").
- **Engine report · playing now** (collapsed): the format running now · the number of clipped samples · if it differs from the chosen format, "applies from the next start".
- Under a **Rejected by the engine** row, the reason the engine gave appears on one line: no row in the format table · macOS left the playback format as Float32 ·
  DAC volume is not at maximum · the format came back different · could not change the rate · another app holds the DAC exclusively · the DAC is not in the list. The trailing
  `(이유 N · 코드 M)` ("(reason N · code M)") is the number the engine gave. Because the engine's PCM output is always opened exclusively, in a check made in the shared state it does not reject merely because macOS
  insists on Float32 — when playback starts it sets the integer format again, exclusively.
- **On DACs where macOS leaves the playback format as Float32 even with exclusive access** (FiiO K15 and others), PCM integer output also works: the engine carries the integer values exactly in
  Float32 — the same way DSD (DoP) does on this DAC. In that case, as with DoP, **the macOS volume must be at maximum**
  (if it is within 0.1 dB of maximum, it is set to 1.0 during playback and restored afterward). If it has been lowered, it does not start, with `DAC 음량이 최대가 아니어서…` ("Because the DAC volume is not at maximum…") —
  reduce loudness with the DAC's knob.
- **If the DAC reconnects within N seconds, playback resumes** (the same DAC only; it does not move to another device or to the Mac's speakers). "Don't wait (기다리지 않기)".
- **It starts even if another app is producing sound on the DAC.** The engine takes the DAC exclusively, and only after checking that other apps have moved away from the DAC
  does it set the format — so that nothing else gets mixed into the DSD. If they do not move away within 0.5 seconds, it does not start and shows a sentence that includes that app's name
  **once** (`다른 앱(…)이 DAC에서 물러나지 않아…` — "Another app (…) did not move away from the DAC…"). Fidenne does not quit that app or retry by itself. While the engine holds the DAC,
  macOS moves other apps' sound to another output (usually the Mac's speakers).
- If a PCM integer format is rejected when playback starts, the track-playback-failure line also shows the reason the engine gave instead of a number.

### 7.3 Streaming-app autoplay · Input and output devices

- **After the engine starts**: Choose Auto-detect · Apple Music · Spotify · YouTube Music (browser) · Don't autoplay from the menu. **YouTube Music (browser)** sends ▶ only to an open tab —
  with no tab, or with the browser extension not connected, it turns on the engine only and says so. A newly opened tab may need one ▶ in the browser because of the browser's autoplay rule. TIDAL is not in the list: its app cannot be told to play from outside (its sound still goes through the engine). The first time, macOS may ask you to allow automation — while you answer that window, playback is not counted as failed; it waits.
  - **Auto-detect**: follows the app that is playing (Music · Spotify). **It does not start a new track when you turn on the engine** — so to listen to a browser (YouTube in Edge and so on)
    through the engine, turn on the engine with Auto-detect selected and play in the browser. Start tracks with the play button or in the playback app.
  - **Apple Music · Spotify**: turning on the engine opens that app and plays the current item (as before).
  - **Don't autoplay**: only turns on the engine. The app that was playing keeps playing through the engine.
  - **The engine follows one streaming app at a time.** If Music and Spotify play at the same time, it follows the one that started later and pauses the other —
    because source-rate matching · the upcoming track · macOS Now Playing have to belong to one app. At that point the Music page status line shows `… 재생을 따라가느라 … 재생을
    멈췄습니다` ("… paused … playback to follow … playback"). Fidenne cannot pause a browser, so it is heard together with the streaming app (they are mixed in the engine).
- **Input**: Fidenne Inlet is listed first when it is installed or selected, followed by Process Tap and, if you chose one with **+ Another input device**, that device's name. The order does not change the input you have selected. The current input format. The input you choose carries over to the next launch.
  If you have never chosen one, it starts with Fidenne Inlet when that is installed, and with Process Tap otherwise. Even if another loopback app is installed,
  the app does not choose it by itself.
- **+ Another input device (+ 다른 입력 장치)** (one line right under Input): pressing it shows this Mac's input devices (virtual and real); the one you pick becomes a slot of the input and is
  selected at once. It works as a loopback — at start the system output is sent to that device and the engine reads its input — so you can pick only a **device that has both an output and a 2-channel input**: a device with no output (such as a
  microphone), a device whose input is not 2 channels, and the current output DAC are shown greyed out in the list, with the reason. The device you pick is shown on that line by name and removed with **✕**; if it was the input in use,
  removing it switches to Fidenne Inlet (when installed) or Process Tap. Until you pick one the slot is empty. If you picked another input in an older version, that device is already in this slot and is used as it was.
- **Tap target** (when the input is Process Tap): **Whole system** (default — receives a mix of all apps except Fidenne) · **Apple Music** ·
  **Spotify** · **Another app** (a list of apps making sound now — browsers and so on; ↻ to search again).
  **The field for choosing an app exists only in personal builds**. The release version receives only the whole system and no apps appear in the list — to
  receive the sound of just one app, send that app's output to Fidenne Inlet (or a device chosen with +) and choose that as the input. A setting that had an app chosen before is
  changed to the whole system the first time the release version is opened, and `이 배포판에는 앱 지정 탭이 없어 탭 대상을 시스템 전체로 바꿨습니다.` ("This release has no per-app tap, so the tap target was changed to the whole system.") appears once under Tap target.
  In every case, **the received app's sound has its original output blocked while the engine runs and comes out only through the engine** — just that app if you chose an app, and all apps except Fidenne
  (including notification sounds) for the whole system. The browser's sound and the engine's sound do not overlap, and even when the engine takes the DAC exclusively and macOS moves the default output to the Mac's speakers, that
  sound does not leak to the speakers.
  **When you turn off the engine, you hear things as before right away** (the same if Fidenne quits or stops on an error). What you chose applies from the next start. If the chosen app is not
  running, it does not start and shows "실행 중이 아닙니다" ("Not running"). The first time, macOS asks to allow audio recording — if you deny it, no sound is received and
  it is silent (turning off the engine restores things). To allow it again: System Settings → Privacy & Security → Screen & System Audio Recording.
  If Apple Music · Spotify is playing (the position is moving) but the engine has received only complete zeros for 10 seconds, a sentence at the top of the window says where to look for the reason
  (it is not shown for pause · quiet passages · browsers). Being quiet for the length of the buffer (about 0.1 s at Standard) when you turn on the engine is normal (§1).
- **Apple Music source-rate auto-apply** (with Apple Music · Auto-detect): the source rate and the system mixer rate, and a status line.
  Spotify does not report its source rate, so it uses the system input rate — if source-rate auto-apply is on with DSD output,
  switching to Spotify sets the loopback device you chose (Fidenne Inlet by default) to 44.1 kHz.
  - **Track rates remembered**: with a loopback input and DSD output, the rate each Apple Music track actually played at is written per track
    (and per album) on this Mac only (`music-track-rates-v1.json` in the app data folder — sent nowhere). Pressing that track again in Fidenne's
    list sets that rate **before the play command goes out**, so the sound starts at the right rate. A track not heard yet starts at the rate of
    another track of the same album you have heard. When Music moves on to the next track by itself, a remembered rate is also set first. If a
    remembered rate is wrong (for example after changing Music's audio quality setting), that play checks it and corrects it. To clear the
    memory, quit Fidenne and delete that file.
  - **The first sound of a track not heard yet**: pressing a track with no remembered rate in Fidenne's list keeps it **silent for a moment**
    until the rate is known (usually under a second). If the rate is the one already in use the sound starts at once; if not, the rate is
    changed and the track is played again **from the start**. The wait adjusts itself to how long finding the rate takes on this Mac, and is
    2 seconds at most. If the rate is not known by then the sound starts and **that track stays at that rate to its end** (so it does not cut
    out in the middle) — the rate found is remembered for the next time. When Music moves on to the next track by itself there is no wait
    (so an album played through has no gaps between tracks).
- Choosing the output DAC · refreshing. Loopback devices (Fidenne Inlet, and a device chosen with +) do not appear in the DAC list and are not used as the PCM Direct output either —
  sending to them produces no sound.
- **"Fidenne Inlet" as an input** (Fidenne's virtual loopback device — shown only when installed): at start it sends the system output to Fidenne Inlet and the engine reads that device. The path you chose in first-time setup carries over (the default in first-time setup is Fidenne Inlet), and even if a device chosen with + is also there, only the one you chose is used.
  **Notification sounds do not go to Fidenne Inlet; they come from the original notification output device** (it was made unable to become the notification output). A device chosen with + gets the notification sounds too, if that device can be the notification output.
  If you choose it and then remove it, the field stays, that start receives through the system tap, and under the input and in the status line `Fidenne Inlet 이 없어 시스템 탭으로 받습니다.` ("Fidenne Inlet is missing, so receiving through the system tap.")
  appears (the same, with that device's name, when a device chosen with + is missing). It does not fall back to another loopback device. What you chose stays, and if you reinstall, it receives from that device
  from the next launch. What you chose applies from the next start.
- **Installing · removing Fidenne Inlet** (the same field, under "Current input"): a status line (not installed · installed with its version · device visible) and
  **Install… / Reinstall… / Update… (설치… / 다시 설치… / 업데이트…)** · **Remove… (제거…)** · ↻. A signed driver is bundled inside the app, so there is nothing to download separately. Pressing shows a confirmation window once,
  and macOS asks for the **administrator password** (the app does not see the password). Installing · removing restarts the audio service (coreaudiod), so
  **the sound of all apps is briefly cut** — do it when you are not listening. When it finishes, it checks whether the device is visible and reports the result on one line (if it is not visible, it says so).
  It cannot be pressed while the engine is running. If there is a copy installed by hand under the old name (`FidenneWormhole.driver`), it is shown as "옛 이름으로 설치되어 있습니다" ("Installed under the old name"),
  and reinstalling changes it to the new name (the device · input choice stay as they are). If a **different** file with the same name is in that place, it is not touched.

### 7.4 Filter · Modulator · Output gain (card) — sound settings for the DSD path

It has the same shape as the Playback Chain card — a card title, the current settings one line each (**Filter (필터)** · **Output (출력)** (DSD order or PCM bits) · **Gain (게인)**), and one collapsed section
**Details (자세히)** that contains ①–③ below · sound presets · the filter-length guide. Those sections are sections inside the card, so they are not wrapped in separate boxes.

The **"Where should you start listening? (어디서부터 들어볼까요?)"** card is separate, below it — if a recommended combination matches the current settings, its name shows on the **Now (지금)** line, and the recommendation cards are inside the collapsed
**N recommended combinations (추천 조합 N개)**.

**N recommended combinations** — recommendation cards. **They start collapsed every time you launch the app**.
Grouped by purpose: Starting points · Time response · Ringing · High-frequency edge · Band · DSD conversion. Each card has
"What to listen for", and only what is written on the card changes. If you choose while playing, it pauses briefly and resumes. The "Compare processing features ·
DSP page" card below (turning Ostrum on and off · Crossfeed · comparing at the same loudness) only opens the DSP page and does not change settings.

1. **Filter family and length** — processing method (Default SRC / Long-tap extension / Ultra-long-tap — Long-tap has a set of proposals, Ultra-long-tap has one proposal, and the rest are [Experimental]) · family · length. **All filters are shown**
   (the "Also show experimental presets" switch has been removed). [Experimental] means outside the seven proposals, and when you choose one, a badge tells you what to watch out for.
   Badges: Experimental · Caution at 44.1·48 kHz · For high-resolution sources · Passband by input rate — even in a narrow window the badge text is not cut off and the description beside it wraps to the next line.
   The current ultra-long picker offers 262K. The hidden 524K and 1M implementations remain available to the engine.
   Retired lengths are not displayed. **A saved sound preset that pointed to a retired length is moved once, when the app launches, to the closest current length**
   (for example, Cardinal Sinc 524K · 1M → 262K). If something was moved, one line under the saved list says what went where (removed with Close),
   and the list from before the move stays as it was in settings under `aural.soundModes.v1.beforeRetiredFilters`. The engine's filter numbers are unchanged. If you choose a long-tap or ultra-long-tap filter, **"May be out of sync with video · delay ○○ ms"** appears under it — the filter delays the sound by that much and
   the video player does not know it (the number is the engine's design value; the buffer delay is separate). It does not block you. When watching video, the default SRC with the **Low latency** buffer is the least out of sync.
   **Choose by conditions · Cost comparison** (collapsed) — a second way to choose, by cost instead of by name. Four conditions: **Max delay** (No limit · 10 · 50 · 120 · 250 ms) ·
   **CPU limit** (No limit · 5 · 10 · 15 %) · **Pass up to 20 kHz** · **Minimum phase only**. The remaining filters are shown side by side, in order of shortest delay, with delay (peak delay) · ringing (−60 dB before/after) · passband (−0.1 dB) ·
   src CPU, and **pressing a name switches to that filter** — changing only the conditions changes nothing. The list is the same as in the picker above (no retired lengths, and
   experimental filters have "Experimental" next to the name). The filter you currently chose is always shown even if it is outside the conditions, together with "Outside conditions: …". The numbers are based on the current input rate while playing,
   and on 44.1 kHz otherwise. CPU was measured on a machine that was busy with other work, so **read it only as a comparison within the same table**. A filter whose CPU was not measured (Sinc Smooth 8K follow-on) is
   not dropped by the CPU condition and stays as "CPU not measured (CPU 미측정)". The conditions carry over to the next launch. The 20 Hz–18 kHz response is practically the same for all filters — what differs is above 20 kHz and time.
   The **long-tap extension (two-stage filters — 8K–64K and the follow-on versions)** passes the output of the front-stage SRC to the long filter as double (the default since 2026-09-24). It is a measured improvement in which the end-of-chain noise
   drops 0.3–0.6 dB at the −157 dBFS level, and delay · CPU are the same. No audible difference is expected. Single-stage and ultra-long-tap filters are unchanged.
2. **DSD conversion** — modulator **7th order · default** (adaptive) / 5th order · protective, output rate DSD128 / DSD256.
   **The chosen filter · modulator order · experimental dither · buffer carry over to the next launch**. A record that pointed to a retired length is moved to its successor length.
   The output rate is not kept — the starting rate is decided by the "DSD256 starting default" rule below.
   **The usage mode (Music / Video) has been removed** — there is only Music. A sound preset saved earlier as Video is read as Music, and
   the list is rewritten once when the app first launches (the list from before the rewrite stays as it was in settings under `aural.soundModes.v1.beforeDecision100`).
   For anyone who used the **legacy filter** in Video, the conversion filter changes from 16 taps to 208 taps and the sound differs (about 2 ms more delay at 44.1 kHz). Other filters are the same.
   The buffer is chosen separately under "Buffer" below.
   **Buffer** — Low latency · Standard · **Stable (default)** (since 2026-09-28; before that, Standard). The sound quality does not change; only how much is stored up before the sound goes out to the DAC differs. It changes only while stopped and applies from the next playback.
   The chosen buffer carries over to the next launch (previously it returned to the default when you relaunched the app). If you have never chosen one, it is Stable. The dropouts in three days of diagnostic records were not the buffer running empty (underrun) but overload of the device callback interval —
   so since 2026-09-28 the buffer mode also decides the **device callback size**: Low latency 2.5 ms · Standard 5 ms · Stable 10 ms (previously 512 frames in every mode · rate,
   0.73 ms at DSD256). It is clamped within the range the device accepts. The added delay is one callback (a little over 10 ms at most). How much the overload dropped on a real DAC has not been measured yet.
   The line under the picker says only **what you experience** with the chosen mode (the numbers are in the ⓘ at the end of the line). The sound quality is the same in all three.
   - Low latency — "Controls are heard fastest · may drop out when heavy". Output queue about 26 ms · the amount the DAC takes at a time 2.5 ms.
   - Standard — "Between responsiveness and stability". About 105 ms · 5 ms (DSD256 was 93 ms before).
   - Stable — "Recommended · most resistant to dropouts · controls are heard about 0.2 seconds late". About 209 ms · 10 ms (DSD256 was 186 ms before). The queue length and the amount taken at a time are provisional values.
   - If the output briefly runs empty (another program briefly stalls the app · a momentary overload), the engine does not stop; it refills the queue to its initial depth and then continues — it is silent in between.
     Up to three times per minute. The fourth time it stops as before and reports "Output underrun or unstable processing (출력 언더런 또는 처리 불안정)".
   - To hear controls with a short delay, choose Low latency (the same as the old Video buffer). You can also choose Low latency together with a long tap. It does not block this, and shows the combined delay.
   - While playing, one line reported by the engine appears under it. Example: `지금 · 안정 버퍼 209.0 ms + 필터·변환 2.2 ms = 211.2 ms` ("Now · Stable buffer 209.0 ms + filter·conversion 2.2 ms = 211.2 ms"). The lowest value the queue reached (including the last 10 seconds) also appears. If there is a choice that changes from the next start, `· 다음 시작부터 …` ("· from the next start …") is added.
   - If the output ran empty during this playback, a notice appears (Troubleshooting Guide §5). A saved sound preset does not contain the buffer.
   **Experimental · Dither order N (실험 · 디더 N 차)** [Experimental] switch: changes only while stopped and from the next start. **A sound preset contains this switch** —
   loading a preset saved with it on turns it on, and one saved with it off turns it off. The switch's on/off carries over to the next launch (previously it was off when you relaunched the app). A preset saved with it on gets `디더` ("dither") in its title (even the same sound is a different preset if the dither differs). A preset saved before dither was included leaves the switch as it is. It was measured only with the offline · engine mock path and
   was not verified with a DAC · by listening. The DSD256 starting default is DSD256 only after 705.6 kHz DoP has been verified on this DAC.
3. **PCM headroom** — **Auto (recommended) (자동 (권장))** is the default. Just before the modulator (or the PCM integer output), it lowers the whole signal so that peaks raised by EQ · Ostrum do not
   reach the clamp — this is the only gain that prevents clipping, and EQ Preamp · Ostrum Headroom are levels within that stage. Auto value = base −3 dB · the protective 5th order has a lower limit so −1.5 dB more ·
   plus as much as DSP (EQ · Ostrum · Crossfeed) raises the most (including Harmonics) · with an ultra-long-tap filter, −6 dB or lower. Under the switch the value and its breakdown are always shown
   (example: `자동 −9.0 dB = 기준 −3.0 dB · DSP 부스트 −6.0 dB` — "Auto −9.0 dB = base −3.0 dB · DSP boost −6.0 dB"). When you change EQ · Ostrum, it follows over 20 ms, and during A/B · ABX it uses the slot gain and so does not follow.
   Changing it with the slider (−60 … 0 dB, in 0.5 dB steps) · the Mute / −6 / −3 / 0 dB buttons · the shortcut makes it **manual**, and "Return to auto (자동으로 되돌리기)" goes back. If the manual value is higher than the auto value,
   a warning appears. When you relaunch the app it is auto. It is different from the DAC volume — set the audible loudness on the DAC. Auto covers the inter-sample peaks of a 0 dBFS source up to about 2 dB, and
   for larger peaks the counter in Clipping & Headroom shows. **Apply Headroom** in the workbench and a sound preset saved with a manual value also switch headroom to manual.
  **"Why are there three gain controls? — What does each one prevent? (이득 조절이 왜 셋인가요? — 각각 무엇을 막나요?)"** the ⓘ balloon beside it — the balloon's content is in [Explanations §2](EXPLANATIONS.md#2-why-there-are-three-gain-controls--pcm-headroom--eq-preamp--ostrum-headroom).
- **Save current sound preset (현재 사운드 프리셋 저장)** (saves 1 filter + 2 DSD conversion (including experimental dither) + 3 PCM headroom (auto, or a manual value)) · the list of saved sound presets (a preset that contains headroom gets `· 헤드룸 자동` ("· headroom auto") / `· 헤드룸 수동 −N dB` ("· headroom manual −N dB")).
  Loading sets headroom to auto if it was auto, and to the saved value if it was manual. A preset saved before headroom was included leaves headroom as it is. Saving the same sound again with a different headroom replaces the earlier one (one per sound).
- **Current selection guide (현재 선택 가이드)**: What changes / Where to listen / What you accept → filter frequency response graph (§2.5) → collapsed "Details · length·delay and combinations"
  (length · delay · when combined with this modulator·rate). The same sentence is not said twice.
  The filter frequency response graph (full view · transition-band comparison, a software measurement at 44.1 kHz) is shown for **every filter**.
  The ⓘ balloon beside "What changes when the filter length increases? (필터 길이가 늘어나면 무엇이 달라지나요?)" (while the balloon is open, two reference links are shown under it): what stays the same (20 Hz–18 kHz is within 0.0001 dB in every filter · length) · what changes ① the steepness of the 20 kHz
  edge (transition band 1 374 → 223 → 55 → 28 Hz) ② delay (linear phase 2.2 · 18.8 · 33 · 109 · 209 ms, shorter for minimum phase) ③ ringing shape (linear is before and after, minimum phase is only after) ·
  CPU is set by the structure · follow-on versions at 88.2 kHz and above · the delay formula (44.1 kHz, filter length performance table).
- **DSD stabilization notice**: if 7th-order stabilization was triggered, together with the count it offers "Switch to protective 5th order (보호형 5차로 바꾸기)" · "Switch to DSD256 (DSD256 으로 바꾸기)" (only when the DAC accepts it).

### 7.5 Playback Chain · Actual behavior · Diagnostics

- **Playback Chain** card: the same dot and one word as the header window (§2.1) · stage lines · DSP chips · **Details (자세히)** (capture · conversion · band · drops · underruns are inside the lines). When "출력은 안전하게 정지했습니다." ("Output was safely stopped.") appears, press **Reconnect DAC (DAC 다시 연결)**.
- In the **Filter · Modulator · Output gain** card (§7.4), **Details** starts **expanded**, and **Actual behavior · Diagnostics** starts **collapsed**.
- **Actual behavior · Diagnostics** (collapsed): output path · requested rate · actual operating rate · applied signal path · PCM gain readback · PCM sample peak
  (before/after gain) · remaining headroom · memory (RSS) · estimated output buffer delay · input drops / output underruns.
  **Delay is a software estimate** (excluding the OS · DAC · acoustic round trip), and **true peak is an estimate at the 352.8 kHz PCM point** (not an analog measurement at the DAC).

## 8. Settings Window

All app-wide settings are in one place, the **Settings window**. There are three ways to open it — **⌘,** · **Settings…** in the app menu · the gear-shaped **Settings…** row at the very bottom of the sidebar (you can
click anywhere on the row). The window is divided into four tabs, and it reopens on the tab you last viewed. Changes take effect immediately, even during playback, and carry over to the next launch. Each section keeps one line,
and the longer explanation is in the ⓘ at the end of that line (§2.5). "Go to settings (설정하러 가기)" (the two-finger-scroll notice — §2.2) opens the matching tab of this window and briefly highlights that box.

- **General (일반)**: version and **Check for updates… (업데이트 확인…)** · **Interface scale (인터페이스 배율)** (enlarges everything, including buttons · cards · spacing) · **Theme (테마)** (System / Light / Dark) ·
  **Liquid Glass** (on · transparency) · **Playback capsule (재생 캡슐)** (material · transparency) · **Motion effects (동작 효과)** (panel · hover · playback-bar animation — not used if macOS Reduce Motion is
  on) · **Restore default display settings (화면 설정 기본값 복원)** · [Release build] **Help (도움말)** (diagnostics for problem reports — §10).
- **Controls and shortcuts (조작과 단축키)**: changing values with two-finger scroll — while holding ⌘ (default) / when started over the control / off · trackpad haptics Off · Weak · Medium · Strong ·
  **How to use controls (조작법)** row with **Show how to use controls (조작법 보기)** and **Show tips again (팁 다시 보기)** (§2.6) · below that the **shortcut list (단축키 목록)** (§2.4).
- **Sound safety (소리 안전)** and **Privacy (개인정보)** (lyrics internet search · YouTube Music · network destinations) are the items below.
- **Light theme and Liquid Glass**: in Light, like macOS light apps (Finder · Music · System Settings), **the body background is kept
  at the window color (bright white)**, and the transparency slider mainly changes how much the sidebar and glass surfaces show through — this keeps a dark wallpaper from showing through
  and turning the body gray. Cards and the background are separated by faint lines and shadows. Dark is the same as before.
- **Playback capsule**: material **Glass blur (유리 흐림)** (default — shows the most behind it) · **Translucent (반투명)** (blocks the background more so text is legible when overlapping) ·
  **Opaque (불투명)**. Transparency by default follows the Liquid Glass transparency, and moving the slider makes it a value for the capsule alone (turning on "Follow Liquid Glass transparency (Liquid Glass 투명도
  따르기)" makes it follow again). If Liquid Glass is off or macOS Reduce Transparency is on, the capsule is always opaque.
- **Sound safety**: **Volume reminder each time you turn on (켤 때마다 음량 안내)** (default on — even if off, a DAC you use for the first time is asked once) · **Mute if a signal that is not in the music appears (음악에 없는 신호가 나오면 음소거)**
  (output monitoring, default on — normal sound is unchanged). §1.
- **Privacy › YouTube Music**: connection with the Chrome · Edge extension on/off (default off) · **Open extension folder (확장 폴더 열기)** — §8.1.
- **Privacy › Lyrics internet search**: finding lyrics on lrclib.net on/off.
- **Privacy › Network destinations**: turn each internet destination on and off — what goes out · when · what disappears if you turn it off.
- **VoiceOver · Accessibility**: the window's buttons · switches · pop-ups · sliders · number fields each have a name (for example "EQ On", "탭 대상" ("Tap target"), "Reference",
  "Liquid Glass 투명도" ("Liquid Glass transparency") — the value as a percentage). Hint lines are read with the name and the content together — "Recommended Headroom (권장 Headroom)" is followed by −xx dB and the reason.
  This was checked through the accessibility tree by an automatic check, and it has not been listened to directly with VoiceOver.

### 8.1 Using YouTube Music (Chrome extension)

YouTube Music has no Mac app, so you listen in Chrome (or Edge). The sound is received by **Fidenne Inlet** as before and goes to the engine (§7.3).
What is added here is **track information and controls** — Fidenne receives the track name · artist · album · length · position from the YouTube Music tab in Chrome,
shows it in the bottom playback bar as "YouTube Music (브라우저)" ("YouTube Music (browser)"), and the bar's play · pause · next · previous · seek control that tab. Lyrics are also looked up with the same track information.

**One-time setup — install the extension (developer mode)**

1. In Fidenne › **Settings…** › **Privacy** › **YouTube Music**, turn on **Connect with the Chrome · Edge extension (Chrome · Edge 확장과 연결)**.
   (So that the browser can find the app, it writes one small connection file in the Chrome · Edge settings folder. Turning it off deletes it.)
2. In the same place, press **Installation guide… (설치 안내…)**. A small window floats over the browser and shows four steps. In **Chrome** · **Edge** at the top of the window, choose the browser you use (if the default browser is Edge, it opens in Edge).
3. Press **① Copy address (① 주소 복사)**, paste it into the browser's address bar, and press Return — `chrome://extensions` for Chrome, `edge://extensions` for Edge.
4. Turn on **② Developer mode (② 개발자 모드)** — in Chrome it is at the end of the page's top row, in Edge it is a switch at the bottom of the side list.
5. **③** Press the button that appears above once Developer mode is on — in Chrome, **압축해제된 확장 프로그램을 로드합니다** ("Load unpacked"), in Edge, **Load unpacked** (압축을 푼 확장 불러오기 — we did not verify the name on the Korean screen). Press **Copy path (경로 복사)** in the guide window, and in the folder-choosing window, **⌘⇧G** → **⌘V** → Return → **Open (열기)**. The path that is copied is the `Chrome` folder **itself** that you should choose (not the folder above it).
6. **④** Reload the YouTube Music tab that was already open (⌘R). When the bottom line of the guide window changes to **브라우저 1개 연결됨** ("1 browser connected"), you are done.
7. Tab sleeping exception — A browser that puts unused tabs to sleep leaves YouTube Music unable to answer. Add `music.youtube.com` in Chrome under Settings → Performance → Memory Saver → **Always keep these sites active**, or in Edge under Settings → System and performance → Resource controls → **Never put these sites to sleep**.

**Using it**: play a track on music.youtube.com and it appears in Fidenne's bottom bar. If the settings row reads "켜짐 · 브라우저 1개 연결됨" ("On · 1 browser connected"), it is connected.

**Adding from the browser to Fidenne**: on music.youtube.com, right-click (two-finger click) a track row, or press the ⋮ at its end, and the site's menu gets **Add to Fidenne (Fidenne에 추가) ›** at the bottom — opened, it shows `Liked (♥)` first and then Fidenne's YouTube Music playlists by name; picking one adds that one track. On a playlist page or a playlist tile there is **Add this list to Fidenne (이 목록 Fidenne에 추가)**, which brings the list in as a Fidenne playlist (the tracks drawn on the page are taken, and more as you scroll — up to 5000 tracks). If the site's menu cannot be found, the browser's own right-click menu (**이 곡 Fidenne에 추가 ›** · **이 목록 Fidenne에 추가**) does the same. Nothing is read or sent until you press, and album · artist pages do not work yet.

**Playing from the Music page**: pressing the service button in front of the Music page search field shows the service list — each service has its logo and name, and under that the connection status (✓ on the one chosen now). You can press anywhere on the row. Choosing **YouTube Music** makes that page the YouTube Music side.

- The **status line** at the very top shows how things stand now and one thing you can do (for example `Chrome 이 꺼져 있습니다 · 곡을 누르면 뒤에서 엽니다` — "Chrome is off · pressing a track opens it in the background"). Under it are the track playing now and previous · play · next.
  The line speaks using the name of the browser you use — if the default browser is Edge (or only Edge is on or installed), it says things like `Edge 가 꺼져 있습니다` ("Edge is off") and pressing a track opens Edge. If it cannot tell which one, it says `브라우저` ("browser") and opens Chrome.
- **My playlists · Albums**: imported playlists (those imported into the library — §4.1) are shown on the same rows as the Apple Music · Spotify lists. Pressing a list opens its track list; **Play all (전체 재생)** · **Shuffle (셔플)** plays it as a whole, and pressing a track plays in order starting from that track (in the YouTube Music tab). While playing, the following tracks of that list are shown in the **Up next (다음 재생)** list, and pressing one goes to that track.
  For Takeout lists · albums · shuffle · search results, Fidenne sends the next track when a track ends (the bar's next · previous also follow that list).
  For a track played directly in the browser (including radio · autoplay), the YouTube Music page's queue also appears in **Up next** — it is a copy of the page's "Next tracks" list, so it is view-only, and there is nothing yet that goes anywhere when pressed. If there is a list that Fidenne played, that comes first.
  **Albums** are groups made by the album name of the imported tracks
  (the album name is in the library songs file in Takeout).
- **A playlist opened in YouTube Music**: when the extension is connected and you open a playlist screen in YouTube Music, the tracks visible on that screen (title · artist · length) and the list name are stored in Fidenne and appear at the top of **My playlists**, as in `12곡 · 브라우저에서 · 9월 29일 오후 9:04` ("12 tracks · from the browser · Sep 29, 9:04 PM"). No Google Cloud setup is needed.
  Only the tracks the page shows at first come — if the list is long, scrolling to the end in YouTube Music brings more (up to 500 tracks per list). If you open the same list again, the tracks seen then are replaced with fresh ones from the front, and later tracks you did not see because you did not scroll stay as previously received — if the first part changed (tracks removed or the order changed), `일부만 새로 받음` ("Only partly refreshed") is added to the subtitle, and scrolling to the end receives everything anew and it disappears. A track removed in YouTube Music is also removed in Fidenne when you scroll the list to the end. Fidenne does not turn pages or press anything on the page by itself.
  Pressing the list opens its track list, and **Play all** · pressing a track has YouTube Music play it as that list. Inside the list, **Delete list (목록 지우기)** deletes it from Fidenne only — the list in YouTube Music is left as it is. Even if you turn off the extension, saved lists remain.
- **Library (Liked songs · My playlists · Albums · Artists)**: when you open that screen yourself in YouTube Music (Library › Playlists · Albums · Artists, or the music marked as liked), the extension reads what the screen has drawn. Fidenne does not open or scroll screens by itself — for a long screen, scrolling to the end brings more (up to 500 items per screen).
  **Liked songs** is a track list — **Play all** · pressing a track has YouTube Music play it as that list. Under **My playlists** the lists received from the library screen follow — pressing a list whose tracks have not been received yet opens that list in the browser, and when the tracks arrive they show in that place. **Albums** · **Artists** are lists that show the names and subtitles (`앨범 • 아티스트 • 2021` — "Album • Artist • 2021") from the library screen — pressing them does not open anything (the tracks on album · artist screens are not received). At the very top of each group, the received count and time are shown, as in `12개 · 브라우저에서 · 9월 29일 오후 9:04` ("12 items · from the browser · Sep 29, 9:04 PM"), and when re-receiving changed the first part, `일부만 새로 받음` ("Only partly refreshed") is added (it disappears when you scroll to the end). A group with nothing received shows a one-line notice.
- **If there are no lists at all**: `YouTube Music 에서 재생 목록을 열면 여기에 나타납니다` ("When you open a playlist in YouTube Music, it appears here") on one line and a collapsed **Other ways — Google account · Takeout (다른 방법 — Google 계정 · 테이크아웃)** are shown. Expanding it shows the button that imports a Takeout CSV — the same as **YouTube Music library (YouTube Music 보관함)** at the bottom of the lists when there are some (§4.1).
- **It works even if Chrome is off**: pressing a track has Fidenne launch Chrome in the background (without bringing it to the front) to open that track, wait for the extension to attach, turn on the engine (if it is off), and check that it is playing. A Chrome that was already open is not hidden.
  If the browser blocks the first playback (autoplay rules · signed out), it tries once more, and if that still fails, `브라우저가 첫 재생을 막았습니다 · 탭에서 ▶ 한 번` ("The browser blocked the first playback · press ▶ once in the tab") and **브라우저에서 ▶ 한 번** ("Press ▶ once in the browser") appear — pressing it brings that tab to the front (it does not reload). Once you press ▶ **once** in that tab, from then on the bar's play · pause · next · previous are listened to.
  **Why the first time has to be pressed in the browser**: a browser does not let a page that no person has ever pressed make sound by itself (the autoplay rules). Fidenne's buttons go through the extension, so they are not "pressed by a person" — no extension can substitute for that. If the bar's button is blocked by this rule, Fidenne notices and shows the line above. In Edge, putting music.youtube.com under **Allow** at `edge://settings/content/mediaAutoplay` may make even this one time unnecessary (needs confirmation).
- **Search**: type in the **Search in YouTube Music (YouTube Music 에서 검색)** field and press Return. **View in YouTube Music (YouTube Music 에서 보기)** opens the same search in the tab. The results open in the YouTube Music tab.
- Even without the extension you can open a track's address — if the switch is off, Chrome comes to the front and opens that track. Track information · controls require the extension. If there is no Chrome, it opens in the default browser.
- If the capture input is not **Fidenne Inlet**, it tells you on one line — it changes only when you press **To Fidenne Inlet (Fidenne Inlet 으로)** (Fidenne does not change it by itself).
- For an Apple Music · Spotify track, or a track in the listening history, whose same track in YouTube Music is known, the track menu (⋯) has **Open in YouTube Music (YouTube Music에서 열기)**.
- The source row of the Playback Chain shows the browser the tab is running in (when exactly one browser is making sound), the codec the page receives (Opus · AAC), and the volume inside the page, as in `YouTube Music (Chrome) · Opus · 페이지 음량 100 %` ("YouTube Music (Chrome) · Opus · page volume 100 %").
  If the page volume is not 100 % or it is muted, it is shown in orange — the sound is reduced before it leaves the browser, so raise YouTube Music's volume bar all the way (Fidenne does not change it). The rate is in the capture line — Chrome outputs at the output device's rate. The source row in **Details** writes that rate, as in `YouTube Music (브라우저) · Chrome 48 kHz` ("YouTube Music (browser) · Chrome 48 kHz").

**Sound quality — set once if you have Premium**: in the YouTube Music web page, profile picture in the header → **Settings** → **Playback & restrictions** (재생 및 제한사항 on the Korean screen) → set **Audio quality** to **High**.
The menu names are transcribed from the public help — if they differ on your screen, choose a similar name (marked as needing confirmation). Ad-free playback is with Premium. While an ad plays, Fidenne does not show track information and says only "광고 중" ("Ad playing").

- **Likes**: if the track is one you liked in YouTube Music, a small heart appears beside the track name in the bar (view-only — there is nothing yet to press in the bar).
- **What goes back and forth**: track name · artist · album · length · position · whether it is playing, playlist · page volume and mute · codec · whether it is liked, the queue (name · artist · length of up to the next 50 tracks), and the **album art**. The extension only reads what the page already shows on screen and sends no further requests to YouTube. For the art, the extension reads what the browser has already received from the image address the page uses (two of YouTube Music's image servers) (without cookies, usually from the browser's cache), shrinks it to a small JPEG (400 pixels on the longest side, 64 KB or less), and sends it. Fidenne shows that art in the bar · the large playback screen · lists, keeps it only in memory (does not write it to a file), and does not go to the internet by itself to fetch art.
  Track information travels only inside this Mac. **While an ad plays, neither track information nor art is sent.**
- **The bar's progress**: the bar's position and length use the track position that the YouTube Music page reports to macOS (if absent, the `0:03 / 3:45` in the bar below the page) — a new track starts from 0, and when it pauses it stops where it paused.
- **Together with Apple Music · Spotify**: the one that is playing appears in the bar. If both are playing, the one that started later; if both are paused, the one that played last.
- **Control Center's Now Playing**: for YouTube Music tracks, Chrome posts it itself, so Fidenne does not post separately (so the same track does not appear twice). The keyboard's play key is received by Chrome.
- **Edge**: choosing **Edge** in the installation guide window shows Edge's steps. It writes the connection file only when Edge is installed.
- **After you update the app**: when Fidenne starts, it replaces the copy in the extension folder with the new version — pressing the extension's reload (↻) **once** at `chrome://extensions` (`edge://extensions` for Edge) makes it the new version. If the browser's extension is the old version, a line `브라우저의 확장이 옛 판(0.1.0)입니다` ("The browser's extension is an old version (0.1.0)") appears on the Music page and in Settings.
  If the line remains, press **Open extension folder** once (the `Chrome` folder opens and its path is copied) and press ↻ again. Album art · bar progress · first-playback guidance · queue · volume · likes require the new-version extension.
- It is not in the web store yet (Developer mode install only). Safari is not supported.

### 8.2 YouTube Music app window — not available now

A way of signing in to YouTube Music and listening inside a Fidenne window does not exist in any version now. YouTube Music is used
with the Chrome · Edge extension of §8.1 — the account stays in the browser, and only track information and controls come into Fidenne inside this Mac.

- Even if you had turned that window on in an earlier version, the new version does not open the window, and tracks · searches on the Music page go to the browser's extension.
- If you signed in through that window in an earlier version, the web storage the window used (cookies · cache) may remain. To delete it, quit Fidenne and then, in Terminal:

  ```sh
  rm -rf ~/Library/WebKit/*/WebsiteDataStore/5c0f7e2a-3b1d-4e8f-9a6c-2d7b8e1f4a90
  ```

  To end the Google-side session too, sign out in the Google account's "Your devices".

## 9. Development · Diagnostics Page [Dev build]

It exists only in personal builds. No automatic sending · it does not change audio playback or routing.

- **AppleEvent executor** counters (executed · dropped · timed out — observations, not errors).
- **Integrated automatic diagnostics**: records app metrics and personal system context in the same run folder. **Mark problem occurred (문제 발생 표시)** (right away if dropouts · stalls · fan noise occur),
  a description of other symptoms (UTF-8, 500 bytes), open the diagnostics folder.
- **Source band record (음원 대역 기록) (3.17)**: only one line per track — input rate · estimated cutoff frequency · confidence (track name · path · time are not written).
- **Support record**: export the legacy-compatible support file · delete the saved compatible record.
- **DSP benchmark**: choose a set of checks and start · cancel · the latest results folder. The results do not replace verification with real playback · a DAC · listening.

## 10. Sending a Support File

- Release version: **Help → Create diagnostics for a problem report… (도움말 → 문제 제보용 진단 만들기…)** or the same button in **Help › Diagnostic bundle (도움말 › 진단 번들)** at the very bottom of Settings › **General (일반)** opens the "Diagnostics for problem reports (문제 제보용 진단)"
  window — start/stop the diagnostic record, **Create bundle and view contents (번들 만들고 내용 보기)**, then **Send by mail (메일로 보내기)** · **Open bundle folder (번들 폴더 열기)** · **Open GitHub issue window (GitHub 이슈 작성 창 열기)**.
  The mail button only opens your mail app with the address, a subject and the questions filled in — you attach the bundle yourself. **Please send the diagnostic bundle by mail — do not put it on a GitHub issue.** Send problem reports to **fidenne.support@gmail.com**.
  The issue-window button exists only when the app has a public repository written in it (if not, only up to the folder). [Dev build] does not have this window and uses the Development · Diagnostics page.
- **Export support diagnostics… (지원용 진단 내보내기…)** in the Diagnostics menu: creates the same bundle and **shows the contents before sending.** The samples are only numbers and true/false, and the bundle holds the songs you listened to in that period (title · artist · service, the latest 200) as `tracks.json`.
  File paths · device names · accounts are not included. Send by mail · open the bundle folder · (if there is a public repository) open the GitHub issue window — **whether to upload, and where to upload,
  is the user's decision, and the app does not send it.**
- For what is good to collect and send, see [Troubleshooting Guide §9](TROUBLESHOOTING.md#9-if-that-still-does-not-work--what-to-collect-and-send).
