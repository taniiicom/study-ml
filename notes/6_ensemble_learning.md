<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
 MathJax.Hub.Config({
 tex2jax: {
 inlineMath: [['$', '$'] ],
 displayMath: [ ['$$','$$'], ["\\[","\\]"] ]
 }
 });
</script>

# ensemble learning / アンサンブル学習

### 22140026 / 情報科学科

### Tomohiro Tani / 谷 知拓 / mail@taniii.com / https://taniii.com

### 2024.5.31

---

> アンサンブル学習により構築される分類器はなぜ単一の分類器よりも性能が改善することが期待できるのか説明しなさい。

アンサンブル学習において, それぞれの分類器が独立して分類を行うとき, 誤分類する分類器の個数が過半数を超える確率は, 1 つの分類器の誤分類率よりも十分に小さくなるため.

> バギングと AdaBoost の違いについて説明しなさい。

`バギング`:

訓練データを重複を許した複数のランダムサブセットを用いて, 同一のアルゴリズムかつ複数インスタンスで学習し, それらの多数決でクラスラベルを決める手法である.

`AdaBoost`:

複数の弱学習器を順番に学習する手法である.  
まず, 訓練データ全体を用いて学習し, その後, 誤分類したデータに重みをつけ, それを次の学習データとして用いる. この, 重みづけ, 学習のイテレーションを繰り返すことで, 精度を向上させる.

> 3.サンプルコード中の Wine データセットの分類において、バギングによる分類（ただしベース分類器を決定株とし、ベース分類器の個数を 500 とする）と、AdaBoost による分類（ただし弱分類器を決定株とし、弱分類器の個数を 500 とする）の結果を比較せよ。またなぜこのような結果になったのか考察せよ。

---

## notes.

- fix: base_estimator is deprecated.
