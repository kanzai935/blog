### まえがき
とある方の勧めでC言語の勉強を始めた。コンピュータとプログラミングの勉強ができるなんて一石二鳥だと思い、早速勉強を開始した。
題材は以下のkiloというエディタを作るチュートリアルだ。

https://viewsourcecode.org/snaptoken/kilo/index.html

このチュートリアルが結構難しい。キーボードとターミナル間で行われている入出力の処理がいまいちピンとこない。C言語に馴染んでいないのもあるが、なぜこの処理をしなくてはいけない？この定数は何を意味しているの？というのがよくある。逐一調べてはいるが、未消化のものもあるため、記録を兼ねてその疑問点をまとめていく。

## C言語の文法

1. struct
```
struct abuf *ab
```
1. const
```
const char *s
```
1. define
```
#define CTRL_KEY(k) ((k) & 0x1f)
#define ABUF_INIT {NULL ,0}
```
1. unsigned
```
unsigned int i = 0;
```
1. *
```
int *rows
```
1. |=
```
raw.c_cflag |= (CS8);
```
1. ->
```
ab->b
```

## 入出力の処理
1. x1bシリーズ
```
\x1b[2J
\x1b[H
x1b[6n
x1b[K
x1b[?25l
x1b[H
x1b[?25h
```
1. BRKINT
1. ICRNL
1. INPCK
1. ISTRIP
1. IXON
1. OPOST
1. CS8
1. ECHO
1. ICANON
1. IEXTEN
1. ISIG
1. EAGAIN
1. CTRL_KEY
1. ioctl
```
ioctl(STDOUT_FILENO, TIOCGWINSZ, &ws)
```

## 参考資料
https://nxmnpg.lemoda.net/ja/3

### あとがき
kiloがきっかけで、プログラミング(アルゴリズムやデータ構造)への興味が湧いてきた。もっと言うと息の長いエンジニアになるために一からキャリア？を作り直している感覚だ。

良いものを教えてもらいました。

###### ライセンス
```
Copyright (c) 2016, Salvatore Sanfilippo <antirez at gmail dot com>

All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice,
  this list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```
