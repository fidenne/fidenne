<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/EXPLANATIONS.md at commit 60083913fecff876c8e1725df00d19fcb559a621 -->

# Fidenne explanations — why it behaves this way

- This is text to read **when you are curious**, not text to read in the middle of operating the app. For what is where, see the [User manual](MANUAL.md); for how to do something, see the
  [Task guide](HOW-TO.md); if you are stuck, see the [Troubleshooting guide](TROUBLESHOOTING.md).
- The text here was moved over from what had been mixed into the manual, **without shortening it** (the manual cleanup of 2026-09-25). At those places in the manual, links to here remain.

## 1. Why the overload detector's limits differ from AutoEq's numbers

For the detector itself, see the **overload detector (과한 설정 탐지기)** item in [Manual §6.1](MANUAL.md#61-response-graph).

### 1.1 Why the slope limit is not 18 dB/oct

AutoEq's 18 dB/oct (max slope) is a limit applied to the correction curve **before** the filters are fitted,
and it is not applied to the fitted filters — a single filter stage of the kind AutoEq uses (Q 6 · +6 dB) already has a flank of about 32 dB/oct. Previously the detector applied this 18 to the fitted EQ and
**warned about the app's own Auto fit result** (a little over half of the AutoEq fits measured on 100 real headphones, and "635 Hz 21 dB/oct" on a user's screen). Now it warns only about a narrow boost that
a single filter stage cannot produce (for example Q 8 · +6 dB). Auto fit results are also rarely warned about (1–6 of 100), and in that case the AutoEq correction curve itself
is that steep at that spot (beside a dip — a place where AutoEq does not limit the slope). Auto fit itself and the sound did not change.

After that, that "rare warning" appeared on a user's screen (Arashi → Susvara, 4.9 kHz 51 dB/oct) and the correction window could not fix it. The flank was a place that rises from a −4 dB dip to +2.6 dB — the steep part was a **cut**. So now it warns only when not only the combined curve but **the curve of the boost part alone** is that steep. That case is not warned about,
and warnings on Auto fit results dropped to 0–1 of 100 (a narrow boost such as Q 8 · +6 dB is still warned about). When a warning appears, **the improved method of Correction suggestions… (보정 제안…)** fixes it by lowering the Q or gain of the band that creates that flank by the smallest amount.

### 1.2 Why the boost limit is +6.2 dB and above 10 kHz it is an average

AutoEq's +6 dB (max gain) is also a limit that clips the correction curve **before** fitting. AutoEq smooths the curve once more after clipping and itself goes past this to +6.14, it does not apply a limit to the composite curve of the fitted filters (the excess is covered with Preamp), and above 10 kHz it
matches only the average. Previously the detector applied +6.0 to every point of the fitted EQ, and **warned about a little over half of the Auto fit results** measured on 100 real headphones (up to +8.65 dB — mostly shelf overshoot at the 20 kHz end). Now it warns only when it exceeds the 0.2 dB margin AutoEq leaves when it realizes the curve, and above 10 kHz only when the band average exceeds it — of 100, 18 with 10 filters (default), 5 with 16, and
0 with 32 (places where the fitting residual exceeds the margin, at most 0.58 dB). The DF curve on the user's screen had no warning before and has none now. Clipping is handled by PCM headroom auto and the maximum-gain judgment.
**The improved method of Correction suggestions… (보정 제안…)** lowers the exceeded spots to +6.0. Auto fit itself and the sound did not change.

## 2. Why there are three gain controls — PCM headroom · EQ Preamp · Ostrum Headroom

This is what the ⓘ balloon next to **PCM headroom (PCM 헤드룸)** in [Manual §7.4](MANUAL.md#74-filter--modulator--output-gain-card--sound-settings-for-the-dsd-path) shows.

The ⓘ balloon next to **"Why are there three gain controls? What does each one prevent? (이득 조절이 왜 셋인가요? — 각각 무엇을 막나요?)"**: all three lower the overall size, but their positions differ, so what they do differs.
- **PCM headroom** — after all DSP, before the modulator. **What it prevents: clipping** (modulator input limit 0.92 for 7th order · 0.78 for 5th order, PCM full scale). This is the only place where the waveform is actually clipped. Auto by default.
- **EQ Preamp** — at the very front of the EQ (before Ostrum). Not a value that prevents anything but **the level of the EQ**: it is the value an EQ file such as AutoEq brings, and it also decides the size that goes into the Ostrum · Harmonics after it. The calculation inside the app is floating point, so nothing is clipped here.
- **Ostrum Headroom** — inside Ostrum, before Harmonics. **What it prevents: Harmonics overdrive** (the operating point of the harmonic curve). When a recommended Headroom appears, you move it yourself and it does not move by itself.
- Why they are not merged into one: when Ostrum is on, Preamp −6 dB lowers the output peak by only 4.3–7.4 dB (measured with a fake device), and Ostrum Headroom changes the operating point of Harmonics — if you prevent clipping with the first one,
  the Ostrum sound changes. Automatic PCM headroom lowers by only the boost that the first two leave (with an AutoEq file whose Preamp is −6 dB, it stays at −3 dB), so it does not lower twice. Normally you touch none of the three.

## 3. What changed — how it was before

So that the manual states only the current behavior, the "Previously …" sentences that were attached to each section have been collected here. They are in the order of the manual's sections.

- [Manual §2.2](MANUAL.md#22-bottom-playback-bar)
  - **Output settings… · Sound settings… (출력 설정… · 사운드 설정…)**: Previously the DSP page opened, and where you pressed and where the settings were differed.
- [Manual §2.5](MANUAL.md#25-explanations--how-to-read-graphs--glossary)
  - **ⓘ balloon**: Previously the explanation unfolded inside the body as a collapsible, and pressing the ⓘ pushed the controls below it. Now it is a balloon, so nothing is pushed.
- [Manual §6](MANUAL.md#6-dsp-page)
  - **Last notice row (마지막 알림 줄)**: Previously it appeared outside the window below the tabs.
  - **Color of the selected control (선택된 조작의 색)**: Previously it was black in light and white in dark.
  - **Unchanged after visiting another page (다른 페이지에 갔다 와도 그대로)**: Previously all of this disappeared when you left the page, and the Equalizer was reloaded with the engine settings (an empty EQ if not applied). Even then, the engine settings changed only when you pressed **Apply to Engine**.
- [Manual §6.1](MANUAL.md#61-response-graph)
  - **Layers (층)**: The former "target + slope −1 dB/oct" layer was removed.
  - **Headroom · Output in Composite Response (Composite Response 의 Headroom · Output)**: Previously only the Composite Response graph of the Ostrum tab was drawn with Headroom · Output included, so the same curve had two heights on one side.
  - **Position of the Auto fit button (Auto fit 단추 자리)**: Previously it was beside the graph — the "Open measurement…" · target buttons next to it only expanded the files collapsible, so they were removed.
  - **When Auto fit cannot fit (Auto fit 이 못 맞출 때)**: Previously Auto fit only expanded the collapsed section (outside the window), so pressing it seemed to do nothing.
  - **Slope excess warning (기울기 초과 경고)**: Previously the warning promised a correction and the sheet answered "There is nothing to reduce with the EQ (EQ 로 줄일 것이 없습니다)".
- [Manual §6.2](MANUAL.md#62-equalizer)
  - **Preamp recommendation (Preamp 권고)**: Previously the recommendation was the sum of the band boosts, so it recommended −24 dB for an auto-fitted EQ.
  - **Header row of the FIR backend (FIR 백엔드의 머리 줄)**: Previously, once FIR started running, the backend field differed, so it stayed at "Editing · not yet applied (편집 중 · 아직 적용하지 않음)".
  - **First sound of the FIR backend (FIR 백엔드의 첫 소리)**: Previously, every time it started, the original sound went out without EQ while FIR was being prepared (at 48 kHz about 0.4 s for the standard length, about 1.5 s for ×4) — a defect that has been fixed.
- [Manual §6.3](MANUAL.md#63-ostrum)
  - **Fine adjustment of knobs by scroll (노브 스크롤 미세 조정)**: Previously scrolling read only Shift.
  - **Vertical dragging of knobs (노브 세로 끌기)**: Previously it read only rotation, so a straight drag left the value at 0.00.
  - **Engine report row (엔진 보고 줄)**: Previously, for an engine that had received nothing, it wrote "Requested revision 0 has not been applied yet (applied is 1) (요청 리비전 0이 아직 적용되지 않았습니다(적용된 것은 1))".
  - **Graph of Topology Manual (Topology Manual 의 그래프)**: Previously the engine sounded with Manual while the graph drew the Blend curve — fixed.
- [Manual §6.5](MANUAL.md#65-headphone---target--the-auto-eq-row-of-equalizer--advanced--files--treble--llm-collapsible)
  - **Set as target · when it was not applied (목표로 · 적용이 안 됐을 때)**: Previously the reason was only inside the search window and disappeared when it was closed.
  - **Name of Target file type (Target file type 의 이름)**: The former name was "Target type", and it read as the field that changes the current target.
- [Manual §6.6](MANUAL.md#66-bands--strength--auto-fit-the-auto-eq-row-of-equalizer--what-auto-fit-did-collapsible)
  - **Marking of bands over +6 dB (+6 dB 넘는 밴드 표시)**: Reversed on 2026-09-25 — previously a band over +6 dB was shown in orange as "a size AutoEq does not produce".
  - **Slope limit in the LLM prompt (LLM 프롬프트의 기울기 한도)**: Previously the slope limit in the prompt was 18 dB/oct.
- [Manual §6.7](MANUAL.md#67-the-ab-buttons-panel--ab--abx--auto-bypass--loop--level-matched-comparison-음량-맞춤)
  - **Reason for an A/B refusal (A/B 거부의 까닭)**: Previously it ended at "The engine did not start the comparison. Playback is unchanged. (엔진이 비교를 시작하지 않았습니다. 재생은 그대로입니다.)"
  - **A/B on the FIR backend (FIR 백엔드의 A/B)**: Previously FIR always refused with `code 3 (코드 3)`.
- [Manual §7.1](MANUAL.md#71-independent-output-control--output-mode)
  - **When PCM Direct does not know the rate (PCM Direct 가 레이트를 모를 때)**: Previously it did not start and stayed at "Waiting for DAC connection (DAC 연결 대기)".
- [Manual §7.3](MANUAL.md#73-streaming-app-autoplay--input-and-output-devices)
  - **System-wide tap (시스템 전체 탭)**: The former system-wide did not block the original output.
- [Manual §7.4](MANUAL.md#74-filter--modulator--output-gain-card--sound-settings-for-the-dsd-path)
  - **Current selection guide (현재 선택 가이드)**: The former "Design characteristics (설계 특성)" · "Compare it like this (이렇게 비교해 보세요)" were the same sentences as the two rows What changes · Where to listen (무엇이 바뀌나요 · 어디를 들어보나요), so they were removed.
  - **Filter frequency response graph (필터 주파수 응답 그래프)**: Previously the following filters 28–33 had no graph.
