<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->

# 제3자 구성요소 고지 (Third-party notices)

Fidenne 앱과 그 공개 자료는 Fidenne 무료 사용 약관(LICENSE)을 따릅니다. 이 문서는 앱에 들어 있거나 앱이 쓰는
**다른 사람의 구성요소**와 그 라이선스를 적습니다 — 아래 구성요소에는 Fidenne 약관이 아니라 각자의 라이선스가 적용됩니다.

Fidenne and its public materials are under the Fidenne Freeware Licence (LICENSE). This file lists the
components by others that the app contains or uses, and their licences; those components are governed
by their own licences, not by the Fidenne terms.

## 1. 앱에 들어 있는 것 (Included in the app)

### AutoEq — MIT License

헤드폰 보정(EQ)의 계산 순서와 기본 상수는 AutoEq 에서 옮겨 온 것입니다. 소스 파일을 그대로 싣지는 않지만, 옮겨 온
산술과 상수에 대해 아래 저작권 표시와 허가문을 싣습니다. 앱의 EQ 화면 맨 아래 «AutoEq · MIT License» 에도 같은 글이 있습니다.

The headphone correction (EQ) follows AutoEq's processing order and default constants. No AutoEq source file is
shipped; the notice below covers the arithmetic and constants carried over.

- 출처 (Source): https://github.com/jaakkopasanen/AutoEq

```
MIT License

Copyright (c) 2018-2022 Jaakko Pasanen

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

### Sparkle — MIT License (+ 아래 포함 구성요소)

앱 안의 `Frameworks/Sparkle.framework` 는 업데이트 확인과 설치를 맡는 Sparkle 2.10.0 입니다. 공식 릴리스를 그대로 싣고
앱의 서명으로 다시 서명했습니다. 릴리스에 든 LICENSE 전문을 아래에 싣습니다(Sparkle 본체 MIT, bsdiff · bspatch BSD-2-Clause,
sais-lite MIT, Ed25519 구현 zlib 계열).

Sparkle 2.10.0, which checks for and installs updates, is carried as `Frameworks/Sparkle.framework` inside the app: the
official release, re-signed with the app's signature. The LICENSE file of that release follows in full (Sparkle MIT,
bsdiff and bspatch BSD-2-Clause, sais-lite MIT, the Ed25519 implementation zlib-style).

- 출처 (Source): https://github.com/sparkle-project/Sparkle
- 아래 전문에서 한 저작권자의 개인 메일 주소만 뺐다(이름 · 연도 · 조건은 그대로). The one personal e-mail address in the text is left out; names, years and terms are unchanged.

```
Copyright (c) 2006-2013 Andy Matuschak.
Copyright (c) 2009-2013 Elgato Systems GmbH.
Copyright (c) 2011-2014 Kornel Lesiński.
Copyright (c) 2015-2017 Mayur Pawashe.
Copyright (c) 2014 C.W. Betts.
Copyright (c) 2014 Petroules Corporation.
Copyright (c) 2014 Big Nerd Ranch.
All rights reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

=================
EXTERNAL LICENSES
=================

bspatch.c and bsdiff.c, from bsdiff 4.3 <http://www.daemonology.net/bsdiff/>:

Copyright 2003-2005 Colin Percival
All rights reserved

Redistribution and use in source and binary forms, with or withou
modification, are permitted providing that the following conditions
are met:
1. Redistributions of source code must retain the above copyrigh
   notice, this list of conditions and the following disclaimer.
2. Redistributions in binary form must reproduce the above copyrigh
   notice, this list of conditions and the following disclaimer in the
   documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE AUTHOR ``AS IS'' AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED.  IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING
IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.

--

sais.c and sais.h, from sais-lite (2010/08/07) <https://sites.google.com/site/yuta256/sais>:

The sais-lite copyright is as follows:

Copyright (c) 2008-2010 Yuta Mori All Rights Reserved.

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software withou
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

--

Portable C implementation of Ed25519, from https://github.com/orlp/ed25519

Copyright (c) 2015 Orson Peters <orsonpeters@gmail.com>

This software is provided 'as-is', without any express or implied warranty. In no event will the
authors be held liable for any damages arising from the use of this software.

Permission is granted to anyone to use this software for any purpose, including commercial
applications, and to alter it and redistribute it freely, subject to the following restrictions:

1. The origin of this software must not be misrepresented; you must not claim that you wrote the
   original software. If you use this software in a product, an acknowledgment in the produc
   documentation would be appreciated but is not required.

2. Altered source versions must be plainly marked as such, and must not be misrepresented as
   being the original software.

3. This notice may not be removed or altered from any source distribution.

--

SUSignatureVerifier.m:

Copyright (c) 2011 Mark Hamlin.

All rights reserved.

Redistribution and use in source and binary forms, with or withou
modification, are permitted providing that the following conditions
are met:
1. Redistributions of source code must retain the above copyrigh
   notice, this list of conditions and the following disclaimer.
2. Redistributions in binary form must reproduce the above copyrigh
   notice, this list of conditions and the following disclaimer in the
   documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE AUTHOR ``AS IS'' AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED.  IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING
IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.
```

### libmysofa — BSD-3-Clause

헤드폰 공간화에서 사용자가 고른 SOFA(AES69) HRTF 파일을 읽을 때 libmysofa 1.3.5 의 읽기 부분을 씁니다. 파일을 읽어
변환하는 일에만 쓰고, 소리를 처리하는 엔진에는 들어 있지 않습니다. 읽는 쪽 소스는 릴리스 그대로이고, 한 번에 풀어 두는
메모리의 상한을 정하는 작은 수정 하나가 같은 BSD-3-Clause 조건으로 들어 있습니다. 압축을 푸는 zlib 은 macOS 의 것을 씁니다.

The headphone spatialisation reads a person's own SOFA (AES69) HRTF file with the reader part of libmysofa 1.3.5. It is
used only to read and convert that file and is not part of the audio engine. The reader sources are as released, with one
small change that bounds the memory the decoder holds at once, offered under the same BSD-3-Clause terms. Decompression
uses the zlib that comes with macOS.

- 출처 (Source): https://github.com/hoene/libmysofa

```
Copyright (c) 2016-2017, Symonics GmbH, Christian Hoene
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

    (1) Redistributions of source code must retain the above copyright
    notice, this list of conditions and the following disclaimer.

    (2) Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in
    the documentation and/or other materials provided with the
    distribution.

    (3)The name of the author may not be used to
    endorse or promote products derived from this software without
    specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE AUTHOR ``AS IS'' AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY DIRECT,
INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING
IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.
```

### SADIE II Database — Apache License 2.0

헤드폰 공간화의 「가상 스피커」와 「측정 방」은 SADIE II Database 의 피험자 H3 측정값(무향 HRIR, 방 BRIR)에서 만든 두
뱅크를 씁니다. 측정값은 값을 바꾸지 않고 Fidenne 의 뱅크 형식으로 옮겼습니다(위치는 구면 좌표에서 직교 좌표로). 무엇을
바꿨는지와 파일 해시는 뱅크 옆의 `NOTICE.md` 에, 라이선스 전문은 뱅크 옆의 `LICENSE-Apache-2.0.txt` 에 있습니다.
University of York 가 Fidenne 를 보증한다는 뜻이 아닙니다. 두 뱅크와 그 옆의 두 파일은 헤드폰 공간화가 들어 있는 빌드에만
실립니다. 그 기능이 없는 빌드에는 들어 있지 않습니다.

The headphone spatialisation's virtual speakers and measured room use two banks made from the SADIE II Database's subject
H3 measurements (anechoic HRIR, room BRIR). The values were copied unchanged into Fidenne's bank format (positions converted
from spherical to Cartesian coordinates). What was changed and the file hashes are in `NOTICE.md` beside the banks; the full
licence text is in `LICENSE-Apache-2.0.txt` beside them. The University of York does not endorse this product. The two banks
and the two files beside them ship only in builds that include the headphone spatialisation; a build without it carries none
of them.

- 저작권 (Copyright): Copyright 2018, University of York. University of York AudioLab; Gavin Kearney. Measurements: Callum
  Armstrong, Lewis Thresh.
- 출처 (Source): SADIE II Database v2-2, https://zenodo.org/records/12092466 (DOI 10.5281/zenodo.12092466)
- 라이선스 (Licence): Apache License, Version 2.0, http://www.apache.org/licenses/LICENSE-2.0

### xoshiro256** — 공개 영역 (CC0)

디더에 쓰는 난수 생성기는 David Blackman · Sebastiano Vigna 가 공개 영역에 내놓은 xoshiro256** 참조 구현을 다시 쓴
것입니다. 고지 의무는 없지만 출처를 밝힙니다.

The dither's random number generator is a rewrite of the xoshiro256** reference implementation that David
Blackman and Sebastiano Vigna dedicated to the public domain (CC0). No notice is required; the source is named
as a courtesy. https://prng.di.unimi.it/

### YouTube 아이콘 — Google LLC 의 상표 (YouTube Icon, a trademark of Google LLC)

음악 페이지 서비스 목록의 YouTube Music 줄이 Google 이 내놓은 YouTube 아이콘을 고친 데 없이 보입니다. 이 아이콘은 Fidenne 약관이
아니라 YouTube API Services Branding Guidelines 에 따라 쓰며, Google 이나 YouTube 가 Fidenne 를 보증한다는 뜻이 아닙니다.

The service list's YouTube Music row shows the YouTube Icon exactly as Google published it. It is used under the YouTube API
Services Branding Guidelines, not the Fidenne terms, and implies no endorsement by Google or YouTube.

- 출처 (Source): https://brand.youtube/youtube-icon

## 2. macOS 가 제공하는 것 — 앱에 싣지 않음 (Provided by macOS, not shipped)

앱이 링크하는 시스템 라이브러리는 macOS 에 들어 있는 Apple 시스템 프레임워크와 시스템 SQLite · zlib 뿐입니다. 이들은
운영체제의 일부이고 Fidenne 과 함께 배포하지 않습니다. SQLite 는 공개 영역, zlib 은 Zlib 라이선스입니다.

The system libraries the app links are only the Apple system frameworks and the system SQLite and zlib that come with
macOS. They are part of the operating system and are not distributed with Fidenne. SQLite is in the public domain
(https://www.sqlite.org/); zlib is under the Zlib licence (https://zlib.net/).

## 3. 만들 때만 쓴 도구 — 앱에 없음 (Build-time tools, not in the app)

앱의 필터 계수와 시그마델타 변조기 계수는 python-deltasigma · NumPy · SciPy 로 미리 계산해 숫자로 넣은 것입니다.
도구 자체는 앱에 들어 있지 않습니다.

The filter and delta-sigma modulator coefficients were computed ahead of time with python-deltasigma, NumPy and
SciPy and are carried as numbers; the tools themselves are not in the app.

- python-deltasigma (BSD 계열 · BSD-style): Copyright (c) 2009 Richard Schreier · Copyright (c) 2012 Sergio Callegari ·
  Copyright (c) 2013 Giuseppe Venturini and the python-deltasigma contributors
- NumPy, SciPy (BSD-3-Clause)

## 4. 따로 설치하는 것 — 앱에 없음 (Installed separately, not in the app)

- **BlackHole** (GPL-3.0) — 다른 앱과 소리를 주고받는 가상 오디오 장치입니다. Fidenne 은 이것을 싣지도 링크하지도
  않고, 사용자가 직접 설치했을 때 장치 목록에서 찾아 입력으로 고를 수 있게 할 뿐입니다.
  A virtual audio device the user installs; Fidenne neither ships nor links it, and only lists it as an inpu
  when present. https://github.com/ExistentialAudio/BlackHole

## 5. Spotify 로고 (Spotify logo)

Spotify 로고는 Spotify AB의 상표입니다. Spotify에서 제공한 목록의 출처를 표시하기 위해 공식 로고를 변경 없이 사용합니다.
The Spotify logos are trademarks of Spotify AB. Official, unmodified logos identify content provided by Spotify.
[Spotify Design & Branding Guidelines](https://developer.spotify.com/documentation/design).
