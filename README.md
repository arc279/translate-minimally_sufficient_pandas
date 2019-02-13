
https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428
の翻訳(**WIP**)


[pandasクックブック-―Pythonによるデータ処理のレシピ](https://www.amazon.co.jp/pandas%E3%82%AF%E3%83%83%E3%82%AF%E3%83%96%E3%83%83%E3%82%AF-%E2%80%95Python%E3%81%AB%E3%82%88%E3%82%8B%E3%83%87%E3%83%BC%E3%82%BF%E5%87%A6%E7%90%86%E3%81%AE%E3%83%AC%E3%82%B7%E3%83%94%E2%80%95-Theodore-Petrou/dp/425412242X) の著者の方の記事です。

---

# 必要最低限の Pandas

この記事では、データ分析にpandasを使用する際の、私の最適と思う意見を提案します。私の目的は、データ分析のほとんどのケースでは、ライブラリの一部の機能だけで十分であることを主張することです。
ここで紹介する必要十分な最低限の機能は、 pandas の初心者からプロフェッショナルまで役に立つでしょう。
誰もが私の提案に同意するわけではないでしょうが、それらは私の実際のライブラリの使い方、あるいは教えている手法です。
もし、あなたが同意しないか、別の提案があるなら、以下のコメントに残してください。
（訳注：[元記事](https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428)のコメント欄を参照）

この記事を読み終わると

* Pandas の構文などではなく、実際のデータ分析に集中するためには、一部の機能に限定しても十分であることがわかります
* Pandas を用いた一般的な、多岐にわたるデータ分析のタスクに対する、具体的な単一アプローチの指針を持つことができます

## 100時間以上の無料のチュートリアル動画

私は、100時間以上にも及ぶ、Pandas, Matplotlib, Seaborn, そして Scikit-Learn の非常に詳細なチュートリアル動画を公開しています。（2019年の2月より）
ぜひ [Dunder Data YouTube channel](https://www.youtube.com/c/dunderdata) を購読して更新をチェックしてください。

## Upcoming Classes

よりパーソナライズされた授業が必要ならば、今年の3月に予定されている [Machine Learning Bootcamps in NYC](https://www.dunderdata.com/courses) の私のクラスに参加してください。

## Pandas は強力だが使いにくい


