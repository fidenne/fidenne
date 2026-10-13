<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/EXPLANATIONS.md at commit 60083913fecff876c8e1725df00d19fcb559a621 -->

# When you are curious

Read this when you wonder "why does it do that?" For what is where, see the [User manual](MANUAL.md); for how to do something, see the
[Task guide](HOW-TO.md); if you are stuck, see the [Troubleshooting guide](TROUBLESHOOTING.md).

<a id="11-why-the-slope-limit-is-not-18-dboct"></a>
## Why does an overload warning appear?

The detector under the graph on the DSP page looks for places where your current settings make the sound too loud or the curve rise too steeply,
and warns about them. A warning alone does not change the sound.

AutoEq's own curves can slightly exceed these limits too. So the limits are not copied from AutoEq's numbers: the detector warns only about a narrow
boost that a single filter cannot produce, or a spot where both the combined curve and the boost-only curve are steep.
When a warning appears, you can choose how to fix it in **Correction suggestions… (보정 제안…)**.

<a id="12-why-the-boost-limit-is-62-db-and-above-10-khz-it-is-an-average"></a>
## Where does the boost warning start?

It appears where the fitted EQ curve goes above +6.2 dB, which is +6 dB plus the 0.2 dB margin AutoEq leaves when it builds a curve.
Above 10 kHz the band average is judged instead of a single point, because filters cannot follow the curve exactly there.

Clipping (the sound being cut off) is prevented not by this warning but by PCM headroom, below.

## How does EQ correction work?

Only one thing is automatic: **Prevent clipping — lower Preamp automatically (클리핑 막기 — Preamp 자동 낮춤)**, which is off by default. When on, if EQ, Ostrum and crossfeed
add up to more than 0 dB, it lowers only the Preamp by the amount needed. It never touches a band, and the curve keeps its shape.

Corrections that change bands happen only when you press **Apply correction (보정 적용)** in **Correction suggestions… (보정 제안…)**. The window opens on **Industry practice (업계 관례)**: it lowers only the Preamp
and keeps the curve shape. If you choose **Improved (개선)** beside it, only the bands that cause an over-boost or a steep side are changed, by the smallest amount.
Improved shapes the curve, so the window shows a warning and you decide whether to apply it. After applying, **Undo correction (보정 되돌리기)** takes you back once.

## Why does Preamp go down?

Raising a range with EQ makes the whole sound louder and it may be cut off. Preamp lowers everything in advance by that much.
EQ files such as AutoEq's bring this value with them, so turning EQ on may make the sound a little quieter.

To make the shape easy to compare, the DSP graph is drawn without the Preamp. The Preamp is still applied to the sound.

<a id="2-why-there-are-three-gain-controls--pcm-headroom--eq-preamp--ostrum-headroom"></a>
## Why are there three settings that lower the volume?

All three lower the overall level, but they sit in different places and prevent different things.

- **PCM headroom**: at the very end of all processing, it prevents **clipping**. Automatic by default.
- **EQ Preamp**: at the very front of the EQ, it sets the EQ's level. It is the Preamp from the question above.
- **Ostrum Headroom**: inside Ostrum, it keeps Harmonics from being driven too hard. When a recommended value appears, you move it yourself. Only when you turn on **Automatically on every change (바뀔 때마다 자동으로)** beside it (off by default) does the knob follow the recommended value.

They are kept apart because lowering one to protect against one problem would change the sound of another. Automatic PCM headroom lowers only the boost
the first two have not already lowered, so the same amount is never lowered twice. Normally you do not need to touch any of the three.

## How is PCM Direct different from engine output?

With **PCM Direct**, Fidenne does not process the sound. The playback app's sound goes through macOS to the DAC, and the DAC's sample rate is not matched track by track
but set once at start (44.1 kHz for Spotify). If it differs from the track's, macOS converts it. EQ, Ostrum and crossfeed are not applied.

With **engine output** (DSD or PCM 352.8 kHz), the Fidenne engine processes the sound and sends it to the DAC. Even with EQ and the rest all off, the conversions that format needs
(upsampling, modulation, dither, headroom) still apply, so the character of the sound can vary with the filter and modulator you choose.

## Why must the DAC accept 352.8 kHz?

The engine's PCM output is fixed at 352.8 kHz (8 times 44.1 kHz). Engine output cannot be sent to a device that does not accept this format.
Built-in speakers, AirPods, most dongles and monitors are such devices, and they are marked at the end of their names in the output device list.

If you have not chosen a DAC yet, or it has not been confirmed, the app starts in PCM Direct. A DAC that accepts DSD can also be sent DSD.

## Why is Fidenne Inlet installed separately?

Fidenne Inlet is a virtual audio device that music apps can send sound to as if it were a speaker. On macOS such a device is loaded
by the system audio service, not by an app, so it cannot live inside the app; it has to be in the system folder
(`/Library/Audio/Plug-Ins/HAL`). That is why installing it asks for an administrator password once and restarts the audio service,
which briefly stops all sound. Other virtual audio devices are installed the same way.

Inlet is the only thing installed, and Fidenne checks its signature again right before installing it. To remove it, press
**Remove… (제거…)** in **I/O · Diagnostics (입출력 · 진단) › Input and output devices (입력과 출력 장치)**.

If you would rather not install anything, choose **System tap (시스템 탭)** in the first-run setup. It needs no installation, but macOS
hands the sound over converted to 48 kHz. Inlet is recommended because it receives the playing app's original sample rate.
