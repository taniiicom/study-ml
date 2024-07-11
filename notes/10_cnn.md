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

# cnn / 畳み込みニューラルネットワーク

### 22140026 / 情報科学科

### Tomohiro Tani / 谷 知拓 / mail@taniii.com / https://taniii.com

### 2024.6.20

---

> 全結合型ニューラルネットワークと畳み込みニューラルネットワークの違いについて説明しなさい。また、画像認識においてなぜ畳み込みニューラルネットワークが使われるのか説明しなさい。

全結合型ニューラルネットワーク (FCNN) は, 入力層, 隠れ層, 出力層の各層において, 各層のすべてのニューロンが前の層のすべてのニューロンに繋がっているネットワーク構造である.

一方で, 畳み込みニューラルネットワーク (CNN) は, 畳み込み層, プーリング層, 全結合層から構成されるネットワーク構造である. 畳み込み層では, 入力画像に対してフィルタを適用し, 特徴マップを生成する. プーリング層では, 特徴マップをダウンサンプリングすることで, パラメータ数を削減し, 計算量を減らす. 全結合層では, プーリング層で得られた特徴を元に, 入力画像の分類を行う.

画像においては, 各画素の配置や局所的な特徴などの空間情報が重要である. このような空間情報を維持して学習を行うことで精度が向上すること, また, パラメータの数を減ることで計算効率が向上するため, 画像認識においては畳み込みニューラルネットワークが使われる.

> 28×28 の画像を畳み込み層に入力する。フィルタサイズが 5、パディングサイズが 2、ストライドを 2 としたとき、出力される特徴マップの大きさはいくつになるか答えなさい。

14

> ドロップアウト正則化がアンサンブル学習の考え方に近い理由を説明しなさい。

ドロップアウト正則化とは, ニューラルネットワークのトレーニング段階で, ランダムに一部のニューロンを無効化することで, モデルの過学習を防ぐ手法である. テスト時には, すべてのニューロンを使用するが, ドロップアウトに使用した確率に応じて出力をスケーリングする.

アンサンブル学習は, 複数のモデルを組み合わせることで, 予測精度を向上させる手法である.

ドロップアウト正則化は, トレーニング時にランダムに一部のニューロンを無効化することで, 訓練毎に異なるサブネットワークで学習することになるため, これは複数のモデルを学習することに相当するといえる. これにより, モデルの多様性を生み出し, 汎用性能が向上するので, ドロップアウト正則化はアンサンブル学習の考え方に近いといえる.

> サンプルコードの CNN の実装（MNIST 手書き文字認識）に、出力される特徴マップ数が 128、フィルタサイズが 5、パディングサイズが 2 の畳み込み層、RELU 活性化関数、およびサイズが 2 の最大値プーリング層を、全結合層の前に追加し、学習しなさい。学習したモデルを用いてテストデータに対し推論を行い、得られる精度を記載しなさい。また、なぜこのような結果が得られたのか考察しなさい。

### プーリング層の追加前

```txt
Epoch 1 accuracy: 0.9488 val_accuracy: 0.9808
Epoch 2 accuracy: 0.9840 val_accuracy: 0.9878
Epoch 3 accuracy: 0.9891 val_accuracy: 0.9873
Epoch 4 accuracy: 0.9917 val_accuracy: 0.9874
Epoch 5 accuracy: 0.9928 val_accuracy: 0.9885
Epoch 6 accuracy: 0.9942 val_accuracy: 0.9895
Epoch 7 accuracy: 0.9951 val_accuracy: 0.9855
Epoch 8 accuracy: 0.9962 val_accuracy: 0.9892
Epoch 9 accuracy: 0.9966 val_accuracy: 0.9908
Epoch 10 accuracy: 0.9963 val_accuracy: 0.9907
Epoch 11 accuracy: 0.9972 val_accuracy: 0.9893
Epoch 12 accuracy: 0.9969 val_accuracy: 0.9914
Epoch 13 accuracy: 0.9975 val_accuracy: 0.9889
Epoch 14 accuracy: 0.9974 val_accuracy: 0.9913
Epoch 15 accuracy: 0.9980 val_accuracy: 0.9911
Epoch 16 accuracy: 0.9981 val_accuracy: 0.9906
Epoch 17 accuracy: 0.9982 val_accuracy: 0.9912
Epoch 18 accuracy: 0.9973 val_accuracy: 0.9908
Epoch 19 accuracy: 0.9986 val_accuracy: 0.9913
Epoch 20 accuracy: 0.9982 val_accuracy: 0.9909
Test accuracy: 0.9910
```

### プーリング層追加後

```txt
Epoch 1 accuracy: 0.9435 val_accuracy: 0.9821
Epoch 2 accuracy: 0.9862 val_accuracy: 0.9874
Epoch 3 accuracy: 0.9901 val_accuracy: 0.9877
Epoch 4 accuracy: 0.9925 val_accuracy: 0.9886
Epoch 5 accuracy: 0.9932 val_accuracy: 0.9904
Epoch 6 accuracy: 0.9950 val_accuracy: 0.9912
Epoch 7 accuracy: 0.9959 val_accuracy: 0.9883
Epoch 8 accuracy: 0.9963 val_accuracy: 0.9912
Epoch 9 accuracy: 0.9957 val_accuracy: 0.9929
Epoch 10 accuracy: 0.9974 val_accuracy: 0.9904
Epoch 11 accuracy: 0.9967 val_accuracy: 0.9884
Epoch 12 accuracy: 0.9967 val_accuracy: 0.9907
Epoch 13 accuracy: 0.9981 val_accuracy: 0.9916
Epoch 14 accuracy: 0.9983 val_accuracy: 0.9906
Epoch 15 accuracy: 0.9969 val_accuracy: 0.9893
Epoch 16 accuracy: 0.9982 val_accuracy: 0.9917
Epoch 17 accuracy: 0.9980 val_accuracy: 0.9876
Epoch 18 accuracy: 0.9986 val_accuracy: 0.9898
Epoch 19 accuracy: 0.9976 val_accuracy: 0.9911
Epoch 20 accuracy: 0.9982 val_accuracy: 0.9915
Test accuracy: 0.9893
```

### 考察

- 畳み込み層の追加によりモデルの表現力が向上するため, 早い段階で訓練データにより適合したモデルになっていることがわかる. (∵ Epoch 1~5 の accuracy)
- その後は, ドロップアウトによって過学習を抑制されているため, テストデータに対する精度が低下せずに推移していることがわかる. (∵ Test accuracy)

---

## notes.

- なぜ「畳み込み」と呼ばれるか

  数学的に言うと, 畳み込み演算は信号処理や画像処理の分野で広く使用されており, 関数やシグナルに対する畳み込み（convolution）と同じ概念です。具体的には, 畳み込みは 2 つの関数を掛け合わせて積分（または離散的には総和）を取る操作であり, これが CNN におけるフィルタと入力画像との積和演算に対応します。

  このように, CNN はこの畳み込み演算を利用して特徴を抽出するため, 「畳み込みニューラルネットワーク」と呼ばれるのです。
