# 目的関数を定義する (3)

今回，学習したいモデルのは入力 $x$ が与えられた時に出力 $y$ の条件付き確率 $p(y \mid x)$ を出力してくれるようなモデルです。

例えば，入力$x$が犬が写っていれば $p(犬 \mid x) = 0.99, p(猫 \mid x) = 0.01$ となるようなモデルです。

このようなカテゴリ値（離散値）に対する確率分布をモデル化するにはSoftmaxを利用します。

Chainerでは `chainer.functions` で `softmax` 関数が定義されているのでそれを利用できます。

例えば，入力`x`を何らかのモデルで変換しカテゴリ種類数と同じ次元数を持つベクトル`t`を作ります。
次に（必ずしも確率分布となっていない）ベクトル`t`を`softmax`を使って確率分布に変換します。

```
t = model(x)
y = F.softmax(t)
```

## Softmax　(*)

Softmax（または多クラスロジスティックスモデル）とは $d$ 次元の実数値ベクトルから，
$d$ 次元の確率分布を作る方法の一つです。

$softmax(x)$ は，$x$ が $d$ 次元であり，各次元の値が $x[0], x[1], ..., x[d-1]$ の時，

$$y[i]=\frac{\exp(x[i])}{\sum_i \exp(x[i])}$$

と表されます。

あるベクトルvが確率分布となる条件として，

1. 各次元の値が非負
2. 合計値が1

という条件があります。
Softmaxは， $\exp$ が非負であることから1の条件を満たし，各次元の値を足した値で割っていることから2の条件を満たします。
