## はじめに
9月から、とある外部研修にて深層学習を本格的に勉強できることになりました。そのため、**本日 4時間で** 、私用 Mac に Anaconda をベースとした機械学習環境を構築したので、その ~奮闘記~ 記録を書いていきます。


## 前提条件
- Mac OS X ~10.13~ → 10.15
  - SWIG をインストールできなかったので OS ごとバージョンアップ！
- Anaconda3-2019.03
- Python 3.6
  - **Augmentor が Python 3.7 に非対応**

## 大まかにやったこと
1. Anaconda3 のインストール
1. Anaconda によるライブラリのインストール
1. OS が古いせいで、Mecab の Python ラッパー作成ライブラリの SWIG をインストールできなくて凹む
1. Mac OS のバージョンアップ
1. Xcode のインストール
1. Anaconda ではインストールできないライブラリをインストール
1. Mecab のコンパイルとインストール

## 環境構築要件
|ライブラリ|バージョン|Anaconda|
| ---- | ---- | ---- |
|Jupyter Notebook|6.1.1|○|
|Matplotlib|3.0.3|○|
|Numpy|1.16.2|○|
|Pandas|0.24.2|○|
|scikit-learn|0.20.3|○|
|Seaborn|0.9.0|○|
|Pillow|5.4.1|○|
|Tensorflow|1.14.0|○|
|Keras|2.2.4|○|
|Plotly|4.1.1|○|
|Gensim|3.8.0|○|
|**Augmentor**|0.2.3|Anaconda Cloud|
|**mecab-python3**|0.7|Anaconda Cloud|
|**SWIG**|3.0.12|Anaconda Cloud|
|**mecab-ipadic**|2.7.0-200708016|×|
|**Mecab**|0.996|×|

## 苦労したところ
Anaconda からぽちぽちしてインストールできるライブラリは楽勝なんですね。
それ以外の、ライブラリを探したり、コマンドラインでインストールするライブラリや、コンパイルが必要なライブラリで苦労をしました。

### Augmentor
Anaconda Cloud で探して、あったのでインストールしました。

https://anaconda.org/augmentor/augmentor

```sh
# Augmentor を探す
anaconda search -t conda Augmentor
# Augmentor をインストール
conda install -c augmentor augmentor
```

### mecab-python3
Anaconda Cloud で探して、あったのでインスト(ry

https://anaconda.org/temporary-recipes/mecab-python3

```sh
# mecab-python3 を探す
anaconda search -t conda mecab-python3
# mecab-python3 をインストール
conda install -c temporary-recipes mecab-python3
```

### SWIG
最初は brew でインストールしようとしたのですが、OS が古いせいでできず、OS をバージョンアップしたのちに、Anaconda Cloud にあることを知りました。

https://anaconda.org/anaconda/swig

```sh
# SWIG を探す
anaconda search -t conda swig
# SWIG をインストール
conda install -c anaconda swig
```

### mecab-ipadic
brew でインストールしました。

```sh
brew install mecab-ipadic
```

### Mecab
brew でもインストールできないので、ソースをダウンロードしてコンパイルしました。コンパイルのために、新しくした OS で Xcode もインストールしました。

http://taku910.github.io/mecab/#install > UNIX を参照

```sh
tar zxfv mecab-0.996.tar.gz
cd mecab-0.996
./configure
make
make check
sudo make install
```

## Mecab が Jupyter Notebook で動いたよう！
やったね！

```py
import MeCab

mecab = MeCab.Tagger("-Ochasen")
print(mecab.parse("ロイヤルミルクティーはミルクティーよりもカロリーが高い"))

-----------------------------------------------------------------
ロイヤルミルクティー	ロイヤルミルクティー	ロイヤルミルクティー	名詞-一般		
は	ハ	は	助詞-係助詞		
ミルク	ミルク	ミルク	名詞-一般		
ティー	ティー	ティー	名詞-一般		
より	ヨリ	より	助詞-格助詞-一般		
も	モ	も	助詞-係助詞		
カロリー	カロリー	カロリー	名詞-一般		
が	ガ	が	助詞-格助詞-一般		
高い	タカイ	高い	形容詞-自立	形容詞・アウオ段	基本形
EOS
```

## まとめ
Anaconda はとても便利なので、まず Anaconda でライブラリを探しましょう。もしなければ Anaconda Cloud に問い合わせ、それでもなかったら brew 先生に頼り、それでもダメだったら必殺ソースコンパイルをしましょう。
