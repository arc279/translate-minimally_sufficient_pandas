# Overview（WIP）

この記事は
[pandasクックブック-―Pythonによるデータ処理のレシピ](https://www.amazon.co.jp/pandas%E3%82%AF%E3%83%83%E3%82%AF%E3%83%96%E3%83%83%E3%82%AF-%E2%80%95Python%E3%81%AB%E3%82%88%E3%82%8B%E3%83%87%E3%83%BC%E3%82%BF%E5%87%A6%E7%90%86%E3%81%AE%E3%83%AC%E3%82%B7%E3%83%94%E2%80%95-Theodore-Petrou/dp/425412242X) の著者である [Ted Petrou](https://twitter.com/tedpetrou) 氏の以下の記事、

[Minimally Sufficient Pandas](https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428)

を、許可を得て翻訳中のものです。
https://twitter.com/arc279/status/1095511875050033152

不自然な点、間違っている点などがありましたら指摘してもらえると助かります。

以下、翻訳です。

---

# Minimally Sufficient Pandas（必要最低限の Pandas）

この記事では、データ分析にpandasを使用する際の、私の最適と思う意見を提案します。
私の目的は、データ分析のほとんどのケースでは、ライブラリの一部の機能だけで十分であることを主張することです。
ここで紹介する必要十分な最低限の機能は、 pandas の初心者からプロフェッショナルまで役に立つでしょう。
誰もが私の提案に同意するわけではないでしょうが、それらは私の実際のライブラリの使い方、あるいは教えている手法です。
もし、あなたが同意しないか、別の提案があるなら、以下のコメントに残してください。
（訳注：[元記事](https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428)のコメント欄）

この記事を読み終わると

* Pandas の構文などではなく、実際のデータ分析に集中するためには、一部の機能に限定しても十分であることがわかります
* Pandas を用いた一般的な、多岐にわたるデータ分析のタスクに対する、具体的な単一アプローチの指針を持つことができます

## 100時間以上の無料のチュートリアル動画

私は、100時間以上にも及ぶ、Pandas, Matplotlib, Seaborn, そして Scikit-Learn の非常に詳細なチュートリアル動画を公開しています。（2019年の2月より）
ぜひ [Dunder Data YouTube channel](https://www.youtube.com/c/dunderdata) を購読して更新をチェックしてください。

## Upcoming Classes

よりパーソナライズされた授業が必要ならば、今年の3月に予定されている [Machine Learning Bootcamps in NYC](https://www.dunderdata.com/courses) の私の講義に参加してください。

## Pandas は強力だが扱いが難しい

Pandas はデータ分析者の間で最もポピュラーな python のライブラリです。
かなり多くの機能を提供していますが、学習コストが高いライブラリでもあります。
これにはいくつかの理由があります：

* 一般的なタスクをこなすのに複数の方法がある
* DataFrame には240を超えるメソッドと属性がある
* （基本的に同じコードを参照している）お互いのエイリアスであるメソッドがある
* ほぼ同じ機能のメソッドがある
* 同じ目的を達するのに、異なる人によって書かれたさまざまな方法によるチュートリアルが氾濫している
* 一般的なタスクを、慣用的な方法でこなす公式のガイドラインが存在しない
* 公式のドキュメントにも、慣用的でないコードが存在する

## Pandas の必要最低限の機能はなにか？

データ分析ライブラリの目的は、分析者がデータ分析に集中できるツールを提供することです。
Pandas はまさにうってつけのツールですが、分析に集中できるようにはなっていません。
代わりに、ユーザは複雑で過剰な構文を覚えることを強要されます。

私は Minimally Sufficient Pandas の定義として、以下を提案します。

* たいていの要求をこなすことができるのに十分な、ライブラリの機能の一部
* コードの書き方ではなくデータの分析に集中することができること

この Pandas の必要最低限のサブセットでは：

* 単純、明白、直接的で、退屈なコードになるでしょう
* あるタスクをこなすために、ただ1つの明白な方法を選ぶようになるでしょう
* そして毎回、明白な方法を選ぶでしょう
* 脳内の短期記憶に多くのコマンドを覚えておく必要はありません
* 他人やあなたにとって、より理解しやすいコードになるでしょう

## よくあるタスクの標準化

Pandas はしばしば、同じタスクをこなすのに複数のアプローチを提供します。
これは、あなたの取ったアプローチが、他人のそれとは異なるかもしれないことを意味します。
これは、1列のカラムを選択する、などの最も基本的なタスクでも発生する可能性があります。
複数の異なるアプローチを採用しても、個人による単発の分析では、多くは問題にはならないでしょう。
しかし、多人数で長期間かかる分析において、それぞれが異なるアプローチを採用した場合、大混乱を引き起こす可能性があります。

一般的なタスクに対して、標準的なアプローチを採用しないことによって、各自のアプローチの僅かな違いをすべて覚えておくための、大きな認知的負荷が開発者にかかります。
各人が一般的なタスクをこなすために、それぞれの好む方法を採用することは、エラーと非効率を引き起こします。

##  Stack Overflow の雪崩

Stack Overflow で Pandas に関する質問を検索すると、よくある一般的なタスクに対して、複数の競合するさまざまな結果が得られることは、珍しくありません。
DataFrameの列名の変更に関する[この質問](https://stackoverflow.com/questions/11346283/renaming-columns-in-pandas/46912050)には28の回答があります。
あるタスクをこなすために慣用的な方法を1つ知りたい人にとって、この大量の情報に目を通すことは非常に困難です。

## No Tricks

ライブラリの大部分を削ることには、いくつかの（良い）制限があります。
あいまいな Pandas のトリックをたくさん知っていることは、あなたの友達にドヤれるかもしれませんが、たいてい良いコードに繋がることはありません。
それどころか、理解しがたく、そしてデバッグがより困難な長大なコードを生み出すでしょう。

## Pandas の具体例

では、タスクをこなすために複数のアプローチが存在する Pandas の、具体例について説明します。
異なるアプローチを比較対照して、どちらのアプローチが望ましいかについての指針を示します。

トピックは以下のとおりです：

* 単一の列を選択する
* `ix` インデクサは非推奨
* `at` `iat` によるセルの選択
* `read_csv` と `read_table` は重複
* `isna` と `isnull` 、 `notna` と `notnull`
* 算術演算子および比較演算子と、それらに対応するメソッド
* python の組み込み関数と、同名の Pandas の同名のメソッド
* `groupby` による集計方法の統一
* MultiIndex の扱いかた
* `groupby` `pivot_table` `crosstab` の違い
* `pivot` と `pivot_table`
* `melt` と `stack` の類似点
* `pivot` と `unstack` の類似点

## 必要最低限のガイドライン

 具体例は全て以下の原則に則っています。

> あるメソッドが他のメソッドよりも追加の機能を提供していない場合（つまり、その機能が他のメソッドのサブセットである場合）、それを使用するべきではありません。メソッドは、追加の独自の機能がある場合にのみ検討する必要があります。

## 単位の列を選択

Pandas の DataFrameから1列のデータを選択することは、最も簡単なタスクにでありながら、残念ながら、Pandas の提供する複数の手法にユーザが最初に直面するケースです。

ブラケット (`[]`) またはドット表記を使用して、単一の列をシリーズとして選択できます。小さな DataFrame から、両方の方法を使用して列を選択してみましょう。

```py
>>> import pandas as pd
>>> df = pd.read_csv('data/sample_data.csv', index_col=0)
>>> df
```

|以下、使用する簡単な DataFrame のサンプル|
|--|
|![A simple DataFrame to be used for the next several examples](https://cdn-images-1.medium.com/max/1600/1*8lCb76QHqjmEyFfC48i4YA.png "A simple DataFrame to be used for the next several examples")|

### ブラケット表記での選択

DataFrame の括弧の中に列名を指定すると、単一の列が Series として選択されます。

```py
>>> df['state']
name
Jane         NY
Niko         TX
Aaron        FL
Penelope     AL
Dean         AK
Christina    TX
Cornelia     TX
Name: state, dtype: object
```

### ドット表記での選択

あるいは、ドット表記を使用して単一の列を選択することも出来ます。出力は上記と全く同じです。

```py
>>> df.state
```

### ドット表記の問題点

ドット表記には３つの問題点があります。以下の状況では機能しません：

* 列名にスペースが入っているとき
* 列名が DataFrame のメソッドと同じ名前であるとき
* 列名を変数で指定したいとき

### 列名にスペースが入っているとき

もし必要なカラム名にスペースが入っていると、ドット表記では指定することが出来ません。
Python はスペースを変数名、演算子の区切りとして扱うため、したがって、スペースを含む列名は正しい構文として扱われません。
エラーを起こしてみましょう。

```py
df.favorite food
```

![](https://cdn-images-1.medium.com/max/1600/1*0OKIvmwok48pOmEdlFVRyw.png)

列名にスペースを含む列の取得はブラケット表記を用いる必要があります。

```py
df['favorite food']
```

### 列名が DataFrame のメソッドと同じ名前であるとき

列の名前と DataFrame のメソッド名が競合した場合、 Pandas は常に列名ではなくメソッドを参照します。
例えば、列名 `count` はメソッドなので、ドット表記で参照されます。
Python はメソッド自体を参照できるため、実際にはエラーになりません。
（訳注：python の関数は first-class object）
では、メソッドを参照してみましょう。

```py
df.count
```
![](https://cdn-images-1.medium.com/max/1600/1*J1IHQtbpSzgMmEaBu5COjg.png)

初めて遭遇した場合、非常に混乱するでしょう。
1行目に `bound method DataFrame.count of` と記載されています。
これは DataFrame の object の保持する何らかのメソッドである、とPythonは教えてくれます。
メソッド名の代わりに、公式な文字列表現（訳注： `repr()`を適用したもの）を出力します。
多くの人は、この出力を見て、何らかの分析を行った結果だと勘違いするでしょう。
しかしこれは正しくなく、ほとんど何も起こっておらず、ただオブジェクトの表現を出力するメソッドへの参照が作成さました。
それだけです。

ドット表記を使用して、列が Series として選択されなかったことは明らかです。
繰り返しますが、DataFrame メソッドと同じ名前の列を選択するときは、ブラケット表記を使用する必要があります。

```py
df['count']
```

### 列名を変数で指定したいとき

選択したい列名を変数に保持していたとしましょう。
この場合もブラケットを使用することが唯一の手法です。
以下は、列名の値を変数に代入してから、この変数をブラケットに渡す単純な例です。

```py
>>> col = 'height'
>>> df[col]
```

### ブラケット表記はドット表記のスーパーセットである

ブラケット表記は、単一の列を指定する機能としては、ドット表記のスーパーセットです。
ドット表記では扱えない3つのケースを紹介しました。

### 多くの Pandas はドット表記で書かれています。なぜ？

多くのチュートリアルで、単一の列を選択するのにドット表記が使われています。
ブラケット表記のほうが明らかに優れているのに、なぜでしょうか？
[公式のドキュメント](http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#attribute-access)の多くの例に使われていたりしますし、3文字多いタイピングが面倒に感じるからかもしれません。

### ガイドライン：データの列を選択する際にはブラケット表記を使用する

ドット表記はブラケット表記よりも多くの機能を追加せず、使えないシチュエーションも存在します。
そのため、私は決して使いません。
唯一の利点は、3文字少ないキーストロークです。

単一のデータ列を選択する際にはブラケット表記のみを使用することをお勧めします。
この非常に一般的なタスクに対して、アプローチを統一するだけで、 Pandas のコードは遥かに一貫性のあるものになります。

## `ix` インデクサは非推奨です、使ってはいけません

Pandas は行を選択する際に、ラベルでの指定と、整数での位置指定を提供しています。
この一見柔軟な2通りの方法は、初学者にとって大きな混乱の原因になります。
`ix` インデクサは、ラベルと整数位置の両方で行と列を選択するために、Pandas の初期に作成されましたが、
Pandas の行と列の名前は、整数と文字列どちらにもなり得ることがあるため、これはかなり曖昧で有ることが判明しました。

これを明示的に選択するために、 `loc` と `iloc` インデクサが実装されました。
`loc` インデクサーはラベルのみ、 `iloc` インデクサーは整数位置のみに対して使用できます。
`ix` インデクサは多目的でしたが、`loc` `iloc` インデクサの登場により推奨されなくなりました。

### ガイドライン： 全ての `ix` の痕跡を削除し、 `loc` および `iloc` に置き換えてください

## `at` `iat` による選択

DataFrame 内の単一のセルをを選択するために、さらなる2つのインデクサである `at` `iat` が存在します。
これらは、類似の `loc` `iloc` インデクサに比べて、わずかにパフォーマンスの面で優れています。
しかし、それらの機能を追加でさらに覚えておかなければならない負担ももたらします。
また、ほとんどのデータ分析において、大規模でない限りは、パフォーマンスの向上は役に立ちません。
そして、本当にパフォーマンスが問題になるケースでは、DataFrame から NumPyの配列に変換することで、パフォーマンスは大幅に向上します。

### パフォーマンス比較： `iloc` vs `iat` vs `NumPy`

単一セルを選択するケースで、 `iloc`、 `iat`、 NumPy配列のパフォーマンスを比べてみましょう。
ランダムデータを含む 100k行 5列 のNumPy配列を作成します。
それを元に DataFrame に変換して、試してみましょう。

```py
>>> import numpy as np
>>> a = np.random.rand(10 ** 5, 5)
>>> df1 = pd.DataFrame(a)

>>> row = 50000
>>> col = 3

>>> %timeit df1.iloc[row, col]
13.8 µs ± 3.36 µs per loop

>>> %timeit df1.iat[row, col]
7.36 µs ± 927 ns per loop

>>> %timeit a[row, col]
232 ns ± 8.72 ns per loop
```

`iloc` に比べて `iat` は2倍の速度も出ない一方、 NumPy配列では約60倍も速度が向上します。
パフォーマンス要件を満たすアプリケーションが本当にあるのであれば、Pandas ではなく NumPy を直接使用するべきです。

### ガイドライン：単一セル選択に本当にパフォーマンスが必要な場合は、`at` `iat` ではなく、 NumPy配列を使用してください

## メソッドの重複

Pandas には全く同じことをするメソッドが複数あります。
2つのメソッドが内部で全く同じ機能を使用している場合は、常に、それらは互いのエイリアスであると言います。
ライブラリ内で同じ機能の重複は完全に不要であり、名前空間を汚染し、分析者に余計な情報を覚えておくよう強制します。

次のセクションでは、いくつかの重複したメソッド、あるいはよく似たメソッドについて説明します。

## `read_csv` と `read_table` の重複

重複の例として、`read_csv` と `read_table` 関数を挙げましょう。
どちらもテキストファイルからデータを読み込んで、まったく同じことを行います。
唯一の違いは、 `read_csv` がデフォルトのセパレータがカンマであるのに対して、 `read_table` はタブ文字であることです。

`read_csv` と `read_table` が同じ結果になることを確認しましょう。
サンプルデータとして、public な [College Scoreboard dataset](https://collegescorecard.ed.gov/data/) を使用します。
`equals` メソッドは、2つの DataFrameがまったく同じ値を持つかどうかを確認します。

```py
>>> college = pd.read_csv('data/college.csv')
>>> college.head()
```
![](https://cdn-images-1.medium.com/max/1600/1*zdBvIsRRlux5YhAMAcxZNg.png)

```py
>>> college2 = pd.read_table('data/college.csv', delimiter=',')
>>> college.equals(college2)
True
```

### `read_table` は非推奨です

私は、非推奨としたほうが良いと思う関数とメソッドに関して、
[Pandas の Githubリポジトリ](https://github.com/pandas-dev/pandas/issues/18262#issuecomment-346502617) に Issue を出しています。
`read_table` メソッドは非推奨のため、使用しないでください。

### ガイドライン：区切り文字付きテキストファイルを読み込む場合は `read_csv` のみを使用してください

## `isna` vs `isnull` と `notna` vs `notnull`

`isna` `isnull` メソッドはどちらも、DataFrame内に欠損値があるかどうかを判別します。
結果は常に bool 値の DataFrame （あるいは Series）になります。

これらのメソッドは完全に同じです。
一方が他方のエイリアスである、と前の段落で言った通り、両方は必要ありません。
`na` という欠損値を表す文字列が、他に欠損値を扱う `dropna` `fillna` といったメソッド名に追加されたため、 それに合わせて `isna` メソッドも追加されました。
紛らわしいことに、Pandas は欠損値の表現として `NaN` `None` `NaT` を使用していますが、 `NA` は使用しません。

`notna` と `notnull` はお互いのエイリアスであり、単に `isna` の反対を返します。これも両方は必要ありません。

`isna` が `isnull` のエイリアスであることを確認しましょう。

```py
>>> college_isna = college.isna()
>>> college_isnull = college.isnull()
>>> college_isna.equals(college_isnull)
True
```

### 私は `isna` `notna` しか使いません

サフィックスに `na` が付いているメソッドを使用することで、他の欠損値メソッド `dropna` `fillna` の名前と整合が取れます。

Pandasは bool 値の DataFrame を反転するための演算子 `~` を提供しているため、`notna` の使用を避けることもできます。

### ガイドライン： `isna` と `notna` を使いましょう
（訳注）`isnull` `notnull` ではなく

## 算術演算子、比較演算子とそれに対応するメソッド

全ての算術演算子には、同等の機能を提供するメソッドがあります。

（訳注：表にしました）

|op|method|
|-|-|-|
|+|`add`|
|-|`sub` `subtract`|
|*|`mul` `multiply`|
|/|`div` `divide` `truediv`|
|**|`pow`|
|//|`floordiv`|
|%|`mod`|

全ての比較演算子にも、同等の機能のメソッドがあります。

|op|method|
|-|-|-|
|>|`gt`|
|<|`lt`|
|>=|`ge`|
|<=|`le`|
|==|`eq`|
|!=|`ne`|

`ugds` 列（*undergraduate population* の略）のSeriesを選択し、100を加えることで、
`+` 演算子とそれに対応するメソッドの両方で同じ結果が得られることを確認しましょう。

```py
>>> ugds = college['ugds']
>>> ugds_operator = ugds + 100
>>> ugds_method = ugds.add(100)
>>> ugds_operator.equals(ugds_method)
True
```

### 各学校の zスコアを計算する

もう少し複雑な例を見てみましょう。
以下では、 *institution* 列をインデックスにセットして、`SAT` 列を選択します。
これらのスコアを提供していない学校は `dropna` で落とします。

```py
>>> college_idx = college.set_index('instnm')
>>> sats = college_idx[['satmtmid', 'satvrmid']].dropna()
>>> sats.head()
```

![](https://cdn-images-1.medium.com/max/1600/1*n3o0CmDXaQxFQ0VlHbNtDA.png)

各大学の SATスコアの z-score に興味があるとしましょう。
（訳注：名前が紛らわしいですが [z-score](https://ja.wikipedia.org/wiki/%E6%A8%99%E6%BA%96%E5%BE%97%E7%82%B9) はいわゆる偏差値で、SATスコアが計算対象のスコアです）
これを計算するには、平均値を引き、標準偏差で割る必要があります。
まず各列の平均と標準偏差を計算しましょう。

```py
>>> mean = sats.mean()
>>> mean
satmtmid    530.958615
satvrmid    522.775338
dtype: float64
>>> std = sats.std()
>>> std
satmtmid    73.645153
satvrmid    68.591051
dtype: float64
```

算術演算子を使った計算結果を見てみます。

```py
>>> zscore_operator = (sats - mean) / std
>>> zscore_operator.head()
```
![](https://cdn-images-1.medium.com/max/1600/1*JYPrbX1Jd6HFTOmAL3aN-g.png)

メソッドを使った方法も算出して、結果を比べてみましょう。

```py
>>> zscore_methods = sats.sub(mean).div(std)
>>> zscore_operator.equals(zscore_methods)
True
```

### 実際にメソッドが必要になる場合

いまの所、演算子よりもメソッドを使ったほうが良い場面には出会ったことがありません。
メソッドを使用する場合でしか対応できないケースを見てみましょう。
college データセットには、学部生の人種の相対頻度である連続値の列が9つ含まれています。
`ugds_white` から  `ugds_unkn` までです。
これらの列を新たな DataFrame に取り出しましょう。

```py
>>> college_race = college_idx.loc[:, ‘ugds_white’:’ugds_unkn’]
>>> college_race.head()
```
![](https://cdn-images-1.medium.com/max/1600/1*__Co7Qx7JYY1bAeJC2ctJw.png)

学校ごとに人種別の生徒数に関心があるとしましょう。
学部全体の人口に各列を掛ける必要があります。
Series として `ugds` 列を選択しましょう。

```py
>>> ugds = college_idx['ugds']
>>> ugds.head()
instnm
Alabama A & M University                4206.0
University of Alabama at Birmingham    11383.0
Amridge University                       291.0
University of Alabama in Huntsville     5451.0
Alabama State University                4811.0
Name: ugds, dtype: float64
```

そして、先程の `college_race` にこの Series を掛けます。
直感的にはこれでうまくいきそうですが、そう上手くはいきません。
代わりに、7544列の巨大な DataFrame になります。

```py
>>> df_attempt = college_race * ugds
>>> df_attempt.head()
```
![](https://cdn-images-1.medium.com/max/1600/1*X3bdE6iFrFKTLLqrkipLAg.png)
```py
>>> df_attempt.shape
(7535, 7544)
```

### インデックス あるいは 列の自動調整

Pandas のオブジェクト同士の計算は常に、互いのインデックスあるいは列の間で調整が行われます。
上記の操作では、 `college_race`(DataFrame) と `ugds`(Series) を掛け合わせました。
Pandasは自動的に（そして暗黙的に） `college_race` の列を `ugds` のインデックスの値に揃えました。

`college_race` 列の値はどれも `ugds` のインデックス値と一致していません。
Pandasは、一致するかどうかに関わらず、 outer join することによって調整します。
結果は、全ての値が欠損値である馬鹿げた DataFrame になります．
`college_race` DataFrameの元の列名を表示するには、右端までスクロールします。

### メソッドを使うことで調整の方向を変更する

全ての演算子の機能は単一であり、乗算演算子 `*` の機能を私達が変更することは出来ません。
一方メソッドは、パラメータによって操作を制御できるようにすることが出来ます。

### `mul` メソッドの `axis` パラメータを使います

上記で述べた演算子に対応する全てのメソッドには、計算の方向を変更できる `axis` パラメータがあります。
DataFrame の列を Series のインデックスに合わせる代わりに、DataFrame のインデックスを Series のインデックスに合わせることができます。
今からやり方をお見せしましょう。

```py
>>> df_correct = college_race.mul(ugds, axis='index').round(0)
>>> df_correct.head()
```
![](https://cdn-images-1.medium.com/max/1200/1*82_NlxL9Dt_c1BiiJQgB6A.png)

`axis` パラメータのデフォルト値は *columns* に設定されています。
適切な調整が行われるように、それを *index* に変更しました。

### ガイドライン：どうしても必要なときだけ算術/比較メソッドを使い、そうでなければ演算子を使う

算術演算子と比較演算子の方がより一般的であり、こちらを最初に試しましょう。
どうしても演算子では解決できない場合に限り、同等のメソッドを使用しましょう。

## Python 組み込み関数と同名のPandas のメソッド

Python のビルトイン関数と同じ名前、同じ結果を返す DataFrame / Series のメソッドがいくつかあります。これらです：

* sum
* min
* max
* abs

1列のデータでテストして、同じ結果が得られることを確認しましょう。
まず、学部生の人口の列 `ugds` から欠損値を除外します。

```py
>>> ugds = college['ugds'].dropna()
>>> ugds.head()
0     4206.0
1    11383.0
2      291.0
3     5451.0
4     4811.0
Name: ugds, dtype: float64
```

#### Verifying `sum`

```py
>>> sum(ugds)
16200904.0

>>> ugds.sum()
16200904.0
```

#### Verifying `max`

```py
>>> max(ugds)
151558.0

>>> ugds.max()
151558.0
```

#### Verifying `min`

```py
>>> min(ugds)
0.0

>>> ugds.min()
0.0
```

#### Verifying `abs`

```py
>>> abs(ugds).head()
0     4206.0
1    11383.0
2      291.0
3     5451.0
4     4811.0
Name: ugds, dtype: float64

>>> ugds.abs().head()
0     4206.0
1    11383.0
2      291.0
3     5451.0
4     4811.0
Name: ugds, dtype: float64
```

### それぞれの処理時間を測ってみます

#### `sum` performance

```py
>>> %timeit sum(ugds)
644 µs ± 80.3 µs per loop

>>> %timeit -n 5 ugds.sum()
164 µs ± 81 µs per loop
```

#### `max` performance

```py
>>> %timeit -n 5 max(ugds)
717 µs ± 46.5 µs per loop

>>> %timeit -n 5 ugds.max()
172 µs ± 81.9 µs per loop
```

#### `min` performance

```py
>>> %timeit -n 5 min(ugds)
705 µs ± 33.6 µs per loop

>>> %timeit -n 5 ugds.min()
151 µs ± 64 µs per loop
```

#### `abs` performance

```py
>>> %timeit -n 5 abs(ugds)
138 µs ± 32.6 µs per loop
>>> %timeit -n 5 ugds.abs()
128 µs ± 12.2 µs per loop
```

### `sum` `max` `min` のパフォーマンスの違い

`sum` `max` `min` は明確に差が出ています。
Pandas のメソッドが呼び出される時とは違い、Python 組み込み関数が呼び出されるときにはまったく異なるコードが実行されます。
`sum(ugds)` を呼び出すと、各値を1つずつ繰り返すための Python の forループが作成されるのと本質的に同等です。
一方、 `ugds.sum()` を呼び出すと、Cで書かれた Pandas 内部の sumメソッドが実行され、forループで反復するよりもはるかに高速です。

そこまで差が大きくない理由は、Pandas には多くのオーバーヘッドがあることです。
上記の代わりに NumPy array を使用して再度検証すると、10000要素の float の配列で、 Numpy array の sum はPython組み込みのsum関数を200倍ほど上回ります。

### `abs` では結果に差が出ない理由

abs関数と Pandasの absメソッドにパフォーマンスの違いがないことに注意してください。
これは内部でまったく同じコードが呼び出されているためです。
Python は abs関数の挙動を変更する手段を提供しており（訳注： [`__abs__` マジックメソッド](https://docs.python.jp/3/library/operator.html#operator.__abs__)のこと）
、開発者はabs関数が呼び出されるたびに実行されるカスタムメソッドを実装することができます。
そのため、 `abs(ugds)` と書いても `ugds.abs()` を呼び出すことと同等です。それらは文字通り同じです。

### ガイドライン：python 組み込みの同名の関数よりも、 Pandas のメソッドを使う


---

＜＜＜WIP＞＞＞
