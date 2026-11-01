<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from docs/user/EXPLANATIONS.md (0.7.0 edition) -->

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

With **engine output** (DSD or PCM oversampling), the Fidenne engine processes the sound and sends it to the DAC. Even with EQ and the rest all off, the conversions that format needs
(upsampling, modulation, dither, headroom) still apply, so the character of the sound can vary with the filter and modulator you choose.

## Which devices can use engine output?

The engine's PCM output is chosen from supported rates in the 44.1 and 48 kHz families (44.1 to 768 kHz), and a new configuration keeps the source rate by default. A DAC connected directly by USB can be used
if it is a 2-channel device that takes at least one of them (DSD only if that DAC can unpack DoP). A DAC that does not take 352.8 kHz can still be used by lowering the rate to one it takes.
A device that takes none of the supported rates from 44.1 to 768 kHz, or is not 2-channel (some dongles, 4- and 8-channel interfaces), is marked at the end of its name in the output device list and plays only in PCM Direct.

Fidenne processes the sound with EQ, Ostrum, crossfeed and filters and sends it to built-in speakers, the 3.5 mm jack, AirPods (Bluetooth) and HDMI too. macOS mixes the result through its system mixer before sending it to the device, so the data is not bit-identical (**not bit-perfect**).
The engine processes at the highest supported rate from 44.1 to 768 kHz at or below the device's current rate, and macOS converts to the device rate if needed. macOS decides the device's rate and volume; the volume is the Mac's. For a bit-exact output use an external DAC's integer PCM or DSD.

If you have not chosen a DAC yet, or it has not been confirmed, the app starts in PCM Direct. A DAC that accepts DSD can also be sent DSD.

## How is the output rate decided?

The **output rate** is the rate the engine sends to the DAC, and the filters and EQ also run at that rate. If you pick one, every song goes out at that rate.
With **Follow the source's rate family** on, the song's family is followed — a 44.1 kHz-family song (44.1 · 88.2 · 176.4 …) goes out in the 44.1 family and a 48 kHz-family song (48 · 96 · 192 …) in the 48 family,
avoiding a conversion that is not a whole multiple (such as 44.1 → 48). What you choose then is a multiple, and **Auto (highest the device takes)** is the highest multiple the DAC takes.
If a song's rate is not known yet or is only a guess, the family is not changed, and between songs that change family the DAC goes briefly quiet while it locks to the new rate.
Whether a higher rate sounds better has not been checked. At low rates the 24-bit noise margin may fall short of the reference, and the screen says so when it does.

## Why is there silence between songs?

Between songs where the rate changes, the DAC needs time to settle on the new rate, so digital silence is put in front so that the first sound of the new song is not cut.
**Unchanged** leaves the end of the song as it is and puts a short silence in front only when the rate changes. **Smooth** fades the last 0.02 s of a song.
If the first sound is still cut off, make the per-DAC wait (**Wait when the rate changes**) longer. This applies to PCM output of local files.

## Why can an EQ with filters in the treble sound different?

A digital EQ filter is an analog filter carried into the digital domain, and depending on how it is carried the curve bends near half the output rate (Nyquist) and differs from what you set.
The current version computes the coefficients to match their analog prototypes, so at high frequencies (especially above 16 kHz) the curve you set is closer to the real curve. An EQ with filters in the treble
can sound slightly different with the same settings. At 352.8 kHz and in DSD the difference is tiny; it is clearer at low rates such as 44.1 · 48 kHz.

## Why does the DAC rate stay when a track moves on by itself?

Changing a DAC's sample rate means stopping the sound for a moment and opening it again. Doing that while one track runs into the next could cut or pop the sound,
so Fidenne **does not touch sound you are hearing.** When a track moves on by itself and the rate differs, it keeps the current rate and macOS converts.

Matching the rate to a track happens only when you pick the track yourself, before any sound. The rate learned for each track is remembered by service and by evidence
(track · album) and used then. An album with a different release is not treated as the same memory.

## Why does Trellis sometimes stop playback?

Trellis chooses each bit while looking at the sound still to come, so the calculation is heavy. Sound has to reach the DAC at fixed moments;
if this Mac cannot finish the calculation by then, Fidenne stops playback and tells you why instead of sending broken sound. Switching to ‘Precise’,
‘Safe’ or CLANS makes the calculation lighter. Fidenne never changes the method for you; the choice is yours.

## How are Cardinal Sinc 128K and 64K different from other filters?

They are fixed-length sinc filters in the long-tap extension: 128K has about 131,000 taps (delay about 116 ms) and 64K about 65,500 (delay about 70 ms).
Both have a fixed cutoff of 22.05 or 24 kHz, and the twin with **Follow (따라감)** in its name lets the cutoff follow the song's rate.
On 44.1 and 48 kHz songs the twin has the same coefficients and sounds the same; it differs only on songs at other rates.
The longer the filter, the longer the sound takes to come out, so video may drift.

## Where is lyrics translation done?

With translation on, Fidenne tries these in order and drops to the next when one does not work: (1) the AI provider you chose with your own API key (only if you turned it on) →
(2) the Apple model on this Mac (Apple Intelligence, no key, the lyrics never leave the Mac) → (3) macOS translation → (4) the original.
Only (1) sends the lyric lines and the title · artist directly to the chosen provider, and charges go to your account. (2) to (4) send nothing out of the Mac.
Fidenne never quietly switches to another provider because one failed. What goes out is in the [privacy policy](../../../PRIVACY.en.md).
Translations are for your own listening on this Mac; if you publish lyrics or translations elsewhere, that is your responsibility. Lyrics remain the property of their rights holders.

## Why is Fidenne Inlet installed separately?

Fidenne Inlet is a virtual audio device that music apps can send sound to as if it were a speaker. On macOS such a device is loaded
by the system audio service, not by an app, so it cannot live inside the app; it has to be in the system folder
(`/Library/Audio/Plug-Ins/HAL`). That is why installing it asks for an administrator password once and restarts the audio service,
which briefly stops all sound. Other virtual audio devices are installed the same way.

Inlet is the only thing installed, and Fidenne checks its signature again right before installing it. To remove it, press
**Remove… (제거…)** in **I/O · Diagnostics (입출력 · 진단) › Input and output devices (입력과 출력 장치)**.

If you would rather not install anything, choose **System tap (시스템 탭)** in the first-run setup. It needs no installation, but macOS
hands the sound over converted to 48 kHz. Inlet is recommended because it receives the playing app's original sample rate.

## Where does an update connect to?

An update check reads the new-version notice file on github.com. GitHub sometimes hands this file or the new version over to
`release-assets.githubusercontent.com`. For the app's other connections, a pointer to another address is followed only when that
address is allowed. For updates the app checks only the first address, and the update tool (Sparkle) follows what comes after it
itself, so this one place is the exception where the app cannot check the pointer again. A downloaded new version is installed only
when its signature checks out, and only when you choose to install it in the update window. What goes out is in the
[privacy policy](../../../PRIVACY.en.md).

## Why must the Safari extension be opened from the Applications folder?

The Safari extension is inside the Fidenne app, and Safari finds it when the app is in a proper place such as the Applications folder.
An app opened straight from the downloaded .dmg or from the Downloads folder is run by macOS from a separate temporary copy, and Safari
cannot show its extension. Fidenne notices this and says `Safari 확장은 Fidenne을 응용 프로그램 폴더로 옮긴 뒤 다시 열어야 Safari에 보입니다.`
(move Fidenne to the Applications folder and open it again for the extension to appear in Safari).
