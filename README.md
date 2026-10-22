<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->

<p align="center">
  <img src="/docs/user/images/fidenne-icon.png" width="128" height="128" alt="Fidenne 아이콘">
</p>

<h1 align="center">Fidenne</h1>

<p align="center">
  듣던 재생 앱의 소리를 DSP로 다듬어 외장 DAC로 보내는 Mac 앱
</p>

<p align="center">
  <b>공개 베타 1 · 0.6.0 — <a href="https://github.com/fidenne/fidenne/releases/latest">내려받기</a> · <a href="https://fidenne.github.io/fidenne/">설치 · 사용 안내</a></b>
</p>

<br>

<p align="center">
  <img src="/docs/user/images/fidenne-home.png" width="860" alt="Fidenne 음악 화면 — 지금 듣는 곡, 오늘의 청취, 재생목록, 하단 재생 막대 (앨범 표지는 모자이크)">
</p>

<br>

## 어떤 앱인가요

Fidenne 은 듣던 재생 앱의 소리를 DSP로 다듬어 외장 DAC로 보내는 Mac 앱입니다.
Apple Music · Spotify · YouTube Music 등 듣던 앱은 그대로 쓰고, Fidenne 에서 DSP와 DAC 에 맞는 출력 방식을 고릅니다.
음악은 각 서비스의 앱에서 그대로 재생되므로 재생 횟수 집계와 광고는 각 서비스에서 그대로이며, Fidenne 은 광고를 막거나 건너뛰지 않습니다.

<br>

## 소리가 지나가는 길

```
재생 앱  →  Fidenne (EQ · Ostrum · 크로스피드 · 출력 변환)  →  내 DAC
재생 앱  →  macOS  →  내 DAC                                    (PCM Direct)
```

PCM Direct 는 Fidenne 이 소리를 처리하지 않고 macOS 를 거쳐 곧바로 DAC 로 보내는 방식입니다.
지금 어떤 길로 가는지는 앱의 Playback Chain 에서 한눈에 볼 수 있습니다.

<br>

## 할 수 있는 것

- 출력 방식을 DAC 에 맞춰 고릅니다 — DSD(DoP) · PCM 352.8 kHz · PCM Direct.
- EQ · Ostrum · 크로스피드와 필터를 바꾸면서 바로 들어 봅니다.
- 소리가 지나가는 길과 적용 중인 처리를 Playback Chain 에서 확인합니다.
- 듣던 서비스 앱을 Fidenne 에서 조작하고 곡 정보 · 가사를 함께 봅니다(재생은 각 서비스 앱이 합니다).
- 소리는 녹음하지 않습니다.

<br>

## 0.6.0 에서 달라진 것

- 홈과 스트리밍 화면을 새로 짜서 Apple Music · Spotify · YouTube Music 이 같은 모양으로 보입니다. 이어 듣기 · 오늘 들은 것 · 내 재생목록 · 보관함 앨범이 한 화면에 있습니다.
- 재생목록과 앨범의 곡 순서를 끌어서 바꾸고, 앨범을 서비스 라이브러리에 앱에서 저장합니다.
- 가사를 내 API 키(Anthropic Claude · OpenAI · Google Gemini)나 이 Mac 안의 Apple 모델로 번역합니다. 가사 탭에서 들은 곡의 가사와 번역을 모아 봅니다.
- Safari 에서도 YouTube Music 을 씁니다. 확장은 앱 안에 들어 있어 설치할 파일이 없습니다.
- macOS 15 에서도 열립니다(0.5.2 까지는 macOS 26 이상).
- 곡이 저절로 넘어갈 때 DAC 레이트를 건드리지 않고, 시작이 반복해서 멈추면 설정을 지우지 않고 들어가는 복구 화면이 생겼습니다.
- 새 버전을 4 시간마다 확인하고, 업데이트 창에서 설치를 고를 때만 받아 서명을 확인한 뒤 설치합니다.

바뀐 것 전체는 [릴리스 페이지](https://github.com/fidenne/fidenne/releases/latest)에 있습니다.

<br>

## 필요한 것

- Apple 실리콘(M1 이후) Mac 과 **macOS 15 이상**. Intel Mac 에서는 열리지 않습니다.
- **USB 로 직접 연결한 유선 외장 DAC**. DSP(EQ · Ostrum · 크로스피드)와 DSD · PCM 352.8 kHz 출력은 **352.8 kHz 를 받는 2 채널 DAC** 에서 돕니다. 내장 스피커 · AirPods · 대부분의 동글 · 모니터처럼 받지 못하는 장치로는 **PCM Direct**(Fidenne 이 처리하지 않고 macOS 를 거쳐 보냄)로만 듣습니다.
- 앱은 무료입니다.

<br>

## 설치

공개 베타 1 의 0.6.0 입니다. 다음 순서로 설치합니다.

1. 이 저장소의 [릴리스 페이지](https://github.com/fidenne/fidenne/releases/latest)에서 `.dmg` 파일을 받습니다.
2. `.dmg` 를 열고 Fidenne 을 **응용 프로그램** 폴더로 끌어 넣습니다. 디스크 이미지 안이나 다운로드 폴더에서 바로 열지 않습니다(Safari 확장이 보이지 않습니다).
3. 응용 프로그램에서 Fidenne 을 열고, 확인 창이 뜨면 **열기** 를 누릅니다.
4. 처음 설정 창의 안내를 따릅니다. macOS 가 권한을 물으면 허용합니다.

처음 재생하기 전에 DAC 와 앰프의 음량을 낮춰 두세요. 단계별 설명은 [설치 · 사용 가이드](/docs/user/GUIDE.md)에 있습니다.

<br>

## Fidenne 이 쓰는 것

Apple · Spotify · Google 과 관계없는 개인이 만든 무료 앱입니다.

- **Apple Music · Spotify** — 각 앱을 Fidenne 이 대신 조작합니다. Spotify 의 검색 · 재생목록 화면은 Premium 계정과 사용자가 직접 만든 Spotify 개발자 키가 있을 때만 쓰며, 선택 사항입니다. 이 화면의 Spotify 항목은 모두 **OPEN SPOTIFY** 로 Spotify 에서 열 수 있습니다. 연결하지 않아도 Spotify 앱의 소리는 그대로 처리합니다.
- **YouTube Music** — 브라우저 확장으로 연결하는 실험 기능입니다. 사용자가 연 페이지의 곡 정보만 읽고, 광고는 건드리지 않습니다. 읽은 정보는 이 Mac 의 Fidenne 에만 전하고 다른 곳으로 보내지 않습니다.
- **가사 · 헤드폰 측정 · 곡 검색과 차트** — LRCLIB, squig.link, Apple 의 공개 자료를 이 Mac 으로 받아 씁니다. 저작권은 각 권리자와 측정자에게 있습니다.
- **소리** — 이 Mac 안에서만 처리합니다. 녹음하거나 밖으로 보내지 않습니다.
- **앨범 표지와 가사** — 빠른 표시를 위해 이 Mac 에 임시로 두고, 마지막으로 쓴 지 30 일이 지나면 지웁니다. 곡 검색 · 차트의 그림은 메모리에만 둡니다.

전체 목록은 [개인정보 처리 안내](/PRIVACY.md)에 있습니다.

<br>

## 도움

- [설치 · 사용 가이드](/docs/user/GUIDE.md) — 설치부터 쓰는 법까지 순서대로.
- [사용 설명서](/docs/user/MANUAL.md) · [문제 확인 가이드](/docs/user/TROUBLESHOOTING.md) · [알려진 한계](/docs/user/KNOWN_LIMITATIONS.md)
- 문의: fidenne.support@gmail.com
- 권리 · 약관 문의: fidenne.support+legal@gmail.com

## 자주 묻는 질문

**소스 코드를 공개하나요?**
아니요. Fidenne 은 개인 프로젝트로 만들고 있고, 앱의 소스는 공개하지 않습니다. 앱은 계속 무료로 배포합니다.

**확장을 만들 수 있는 SDK 가 있나요?**
지원을 계획하고 있지만 확정된 것은 아니며, 시점도 아직 정하지 않았습니다. 라이선스는 지금 Apache-2.0 을 고려하고 있습니다. 자세한 내용은 공개할 때 알려 드리겠습니다.

## 이슈

버그와 제안은 이 저장소의 이슈로 받습니다. 이슈로 쓰기 어려운 것은 메일 **fidenne.support@gmail.com** 으로 보내 주세요.
보안 문제는 공개 이슈에 쓰지 말고 `SECURITY.md` 의 방법으로 알려 주세요.

제보할 때는 앱의 **도움말 → 문제 제보용 진단 만들기…** 로 만든 지원 파일(보내기 전에 내용을 보여 줍니다)을 메일에 붙이고 무슨 일이 있었는지 한 줄만 적어 주세요. 지원 파일은 이슈에 올리지 않습니다.
**메일로 보내기** 가 메일 앱을 열고, 다른 메일을 쓰면 **메일 양식 복사** 로 주소 · 제목 · 양식을 붙여 넣습니다. 앱 버전과 macOS 버전은 양식과 지원 파일에 저절로 들어 있습니다. 앱은 아무것도 대신 보내지 않습니다.

<br>

<sub>Apple Music은 Apple Inc.의, Spotify는 Spotify AB의, YouTube Music은 Google LLC의 상표입니다. Fidenne은 이 회사들과 관계가 없고 이들의 보증을 받지 않았습니다.</sub>

<sub>무료로 쓸 수 있는 약관을 따릅니다 — `LICENSE`. 앱에 든 제3자 구성요소는 `THIRD_PARTY_NOTICES.md`에 있습니다.</sub>
