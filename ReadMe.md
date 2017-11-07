# このソフトウェアについて

和音名(ChordName)から構成音を音程名(IntervalName)で取得する。

例: Cm7-5 -> P1,m3,d5,m7

後で転回形にできるよう、list型にしておく。tuple型だと変更できなくなってしまう。

# 実行

```sh
$ python Chords.py 
```

`res/`ディレクトリ配下に和音名のパターンを網羅したテキストファイルが生成される。

# クラス関係

すべてクラスであり、クラスメソッドである。以下のような親子関係である。

* Chords.py
    * AnotherChords.py
    * Tension.py
        * Tetrad.py
            * Triad.py

ファイル|説明
--------|----
Chords.py|和音名から構成音の音度名リストを取得する
AnotherChords.py|add,sus,dim,aug系の処理を施す
Tension.py|テンション・ノート付与と7thの暗黙付与
Tetrad.py|四和音の構成音を取得する
Triad.py|三和音の構成音を取得する

# 和音パターン

6万パターン以上。`61892=8+9+124+15+48744+10665+2232+27+6+17+45`。

ファイル名|数|概要|例
----------|--|----|--
chords_3.tsv|8|三和音|m
chords_4.tsv|9|四和音|7
chords_5.tsv|124|五和音(テンション)|(9)
chords_another.tsv|15|add,sus,dim,aug|sus4
chords_3dimaug_7_add.tsv|48|dim|aug + 7th + add|augM7add13
chords_3dimaug_7_tension.tsv|744|augM7(9)
chords_3mM_7_5Pad_sus_add_tension.tsv|10665|M7+5sus4add13(9)
chords_3mM_7_5Pad_tension.tsv|2232|mM7+5(9)
chords_3mM_7_5da.tsv|27|M7+5add4
chords_3mM_add.tsv|6|madd13
chords_3sus_add.tsv|17|sus4add13
chords_7_sus_add.tsv|45|M7sus4add13

# 課題

* 和音パターンを調査し網羅したい
    * 和声音でも未実装パターンがある
        * 名前で取得したい
            * 転回も指定したい
                * omit(音を抜くヴォイシング)も指定したい
        * 同一表記名でも構成音が違う場合があるらしい
            * https://pf-j.sakura.ne.jp/music/chord.htm
        * 音程名だけでなく音度名でも取得したい
            * 音程名: `d7,m7,M7,a7`
            * 音度名: `--7,-7,7,+7`(bb7,b7,7,#7)
        * ピッチクラス(keyId, 半音の数)を取得したい
        * 音程名、音度名、ピッチクラス、間でそれぞれ相互変換したい
        * 半音差しかない構成音がある場合は対象外にしたい
            * 最終的にチェックする関数を用意したい
    * 非和声音は勉強不足。難しそう……
* 12平均律以外の音律でも構成音を算出したいが……
    * 純正律における中間の5音も算出したい。計算方法がよくわからない
* 純正律で綺麗な和音になる主要三和音とそれ以外の音痴な副和音を聴き比べてみたい
* ソースコードが整理できていない
    * 音楽理論がわからず、どうまとめていいのかもわからない

# 開発環境

* Linux Mint 17.3 MATE 32bit
* [libav](http://ytyaru.hatenablog.com/entry/2018/08/24/000000)
    * [各コーデック](http://ytyaru.hatenablog.com/entry/2018/08/23/000000)
* [pyenv](https://github.com/pylangstudy/201705/blob/master/27/Python%E5%AD%A6%E7%BF%92%E7%92%B0%E5%A2%83%E3%82%92%E7%94%A8%E6%84%8F%E3%81%99%E3%82%8B.md) 1.0.10
    * Python 3.6.1
        * [pydub](http://ytyaru.hatenablog.com/entry/2018/08/25/000000)
        * [PyAudio](http://ytyaru.hatenablog.com/entry/2018/07/27/000000) 0.2.11
            * [ALSA lib pcm_dmix.c:1022:(snd_pcm_dmix_open) unable to open slave](http://ytyaru.hatenablog.com/entry/2018/07/29/000000)
        * [matplotlib](http://ytyaru.hatenablog.com/entry/2018/07/22/000000)
            * [matplotlibでのグラフ表示を諦めた](http://ytyaru.hatenablog.com/entry/2018/08/05/000000)

# 参考

感謝。

## 和音

* https://ja.wikipedia.org/wiki/%E5%92%8C%E9%9F%B3
* http://www.piano-c.com/
* https://pf-j.sakura.ne.jp/music/chord.htm

alt,オルタード,1th,3th,5th[#,b],7th[b],9th[#,b]
どれを選んでも構わない。このコードはほとんど見かけず、代わりに数値で具体的に指定する方法がよく見かけます。

msus4,マイナー サスフォー,P1,m3,P4,P5

## 音程

* https://ja.wikipedia.org/wiki/%E9%9F%B3%E7%A8%8B
* https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q1365320628
* https://okwave.jp/qa/q6858420.html

## 440Hz, 432Hz

* http://tabi-labo.com/156689/music-a432

## 和音の生成

* http://ism1000ch.hatenablog.com/entry/2013/11/15/182442
* https://ja.wikipedia.org/wiki/%E4%B8%89%E5%92%8C%E9%9F%B3
* https://ja.wikipedia.org/wiki/%E3%83%91%E3%83%AF%E3%83%BC%E3%82%B3%E3%83%BC%E3%83%89

## 音名

* https://ja.wikipedia.org/wiki/%E9%9F%B3%E5%90%8D%E3%83%BB%E9%9A%8E%E5%90%8D%E8%A1%A8%E8%A8%98

## 音階

* https://ja.wikipedia.org/wiki/%E9%9F%B3%E9%9A%8E

### 五度圏

* http://dn-voice.info/music-theory/godoken/

## 音高の算出

* http://www.asahi-net.or.jp/~HB9T-KTD/music/Japan/Research/DTM/freq_map.html
* http://www.nihongo.com/aaa/chigaku/suugaku/pythagoras.htm

## サイン波のスピーカ再生

* http://www.non-fiction.jp/2015/08/17/sin_wave/
* http://aidiary.hatenablog.com/entry/20110607/1307449007
* http://ism1000ch.hatenablog.com/entry/2013/11/15/182442

# ライセンス

このソフトウェアはCC0ライセンスである。

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)

Library|License|Copyright
-------|-------|---------
[pydub](https://github.com/jiaaro/pydub)|[MIT](https://github.com/jiaaro/pydub/blob/master/LICENSE)|[Copyright (c) 2011 James Robert, http://jiaaro.com](https://github.com/jiaaro/pydub/blob/master/LICENSE)
[pygame](http://www.pygame.org/)|[LGPL](https://www.pygame.org/docs/)|[pygame](http://www.pygame.org/)

