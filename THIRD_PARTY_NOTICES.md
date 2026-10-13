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

앱이 링크하는 라이브러리는 macOS 에 들어 있는 Apple 시스템 프레임워크와 시스템 SQLite 뿐입니다. 이들은 운영체제의
일부이고 Fidenne 과 함께 배포하지 않습니다. SQLite 는 공개 영역입니다.

The app links only the Apple system frameworks and the system SQLite that come with macOS. They are part of the
operating system and are not distributed with Fidenne. SQLite is in the public domain (https://www.sqlite.org/).

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
