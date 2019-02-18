# Overview

この記事は
[pandasクックブック-―Pythonによるデータ処理のレシピ](https://www.amazon.co.jp/pandas%E3%82%AF%E3%83%83%E3%82%AF%E3%83%96%E3%83%83%E3%82%AF-%E2%80%95Python%E3%81%AB%E3%82%88%E3%82%8B%E3%83%87%E3%83%BC%E3%82%BF%E5%87%A6%E7%90%86%E3%81%AE%E3%83%AC%E3%82%B7%E3%83%94%E2%80%95-Theodore-Petrou/dp/425412242X) の著者である [Ted Petrou](https://twitter.com/tedpetrou) 氏の以下の記事、

[Minimally Sufficient Pandas](https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428)

の一部を、許可を得て翻訳したものです。
https://twitter.com/arc279/status/1095511875050033152

全文は「何故そうしたほうが良いのか？」などにも詳しく言及していて長文のため、具体例だけ先に訳しました。
詳しい理由などは元記事を参照してください。
元記事の全文は[現在翻訳中](README.md)です。


不自然な点、間違っている点などがありましたら指摘してもらえると助かります。

以下、忙しい人のための意訳です。

---

# カラム(Series)の選択にドット表記を使わない。ブラケット表記を使う。
* OK) `df[“count”]`
* NG) `df.count`

# `ix` メソッドは使わない
  * ラベルで参照する時は `loc` を使う
  * インデックスで参照する時は `iloc` を使う

# `at` `iat` は使わない

`loc` `iloc` より若干速いが、単一セルの参照にパフォーマンスを気にするなら `numpy.array` に変換した方がよい

# `read_table` は使わない
  * 同じ機能を複数の方法で実現できるのは混乱するので良くない
  * `read_csv` のデリミタを指定する

# na と null

* `isna` と `isnull` は同じ
* `notna` と `notnull` も同じ
  * `isna` `notna` を使う
  * `fillna` `dropna` との整合が取れる

# 算術、比較メソッドは必要な時以外使わない
  * 通常は演算子を使用する
  * `axis` を指定する必要がある場合だけメソッドを使う

# python 組み込みと同名のメソッドは pandas のメソッドを使用する

pandas のメソッドはcで実装されたメソッドを呼んでるので速い。(absだけは同じ)

* OK) `df.sum()`, `df.min()`, `df.max()`, `df.abs()`
* NG) `sum(df)`, `min(df)`, `max(df)`, `abs(df)`

# `groupby` の集計の書き方の統一

`df.groupby('grouping column').agg({'aggregating column': 'aggregating function'})` 方式を使う

（訳注）dictの順序を保持しない python3.6 未満だとカラムの追加される順序が不定になるので注意

# MultiIndex の扱い方

* 非常に扱いが複雑になるので使わないほうが良い（若干のパフォーマンス向上と引換に）
* 単一インデックスに直して扱うと良い（reset_index()を使う）

# `groupby`, `pivot_table`, `crosstab` の違い

* 具体例見た方が早い
* 本質的には同じことをやってる
* `groupby`: 結果が MultiIndex になる
* `pivot_table`: 結果が Single Index + 「集計列のユニーク値」の列になる
    * グループを比較する時は `pivot_table` を使う
* `groupby` は計算の途中経過、`pivot_table` は計算結果、と解釈すると良いのでは
* `crosstab` はカウント用途
    * `pivot_table` とできることは同じ
    * `normalize` パラメータで正規化できる
    * 相対頻度を見る時に `crosstab` を使う

# `pivot` メソッド

* データを整形(縦横の変換)
* 集約はしない。値の重複があるとエラーになる。
* `pivot` は使わず `pivot_table` の使用を検討したほうが良い。

# `melt` メソッド と `stack` メソッド
  * 具体例見た方が早い
  * 横持ちのデータを縦持ちに変換
  * `melt`: インデックスが列に移動するので `set_index` してやる必要がある
  * `stack`: 縦持ちの種別に指定した列をindexとして扱う
  * `stack` より `melt` を使う（MultiIndexを避け列名も指定できる）

# `pivot` メソッド と `unstack` メソッド
  * 具体例見た方が早い
  * MultiIndex の縦持ちのデータを横持ちに変換
  * 列が  MultiIndex になる
  * 代わりに `pivot_table` を使ったほうが良い
