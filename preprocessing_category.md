## 前処理シリーズ3

ここからはカテゴリ特徴量の扱い方を述べていきます。この特徴量の扱い方を学ぶことで、SVMやランダムフォレストなどの特徴量に強く依存する分類器の深い理解にも繋がります。



### カテゴリカルデータの概要

グループで分類される変数をもつデータです。グループでの分類というのが「ミソ」です。
具体的に言うと、データサイエンティストが扱うデータは個数や人数のように数えられるものだけではありません。顧客満足度や好みのように，数えることのできないデータも存在します。それらのデータがカテゴリカルデータです。定性的データと言うとイメージがつくかもしれません。




上述してきた2変数の1次関数の場合でみていきます。Eの最小値を求めるので、「これを偏微分したものが0になる」という方程式を考えればいいということはすでに勉強したと思います。
求める直線（境界線）が<img src="https://latex.codecogs.com/gif.latex?y=ax&plus;b">の時は

<img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;E}{\partial&space;a}&space;=&space;0,&space;\frac{\partial&space;E}{\partial&space;b}&space;=&space;0">


という二つの連立方程式をとけばいいわけです。

・1/2をしている場合

<img
src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;\sum_{i=1}^{N}\frac{1}{2}&space;y_{i}-f(x_{i})}{\partial&space;a}&space;=&space;\frac{\partial&space;\sum_{i=1}^{N}\frac{1}{2}y_{i}-f(x_{i})}{\partial&space;a}&space;=&space;\sum_{i=1}^{N}&space;(y_{i}-a-bx_{i})(-1)&space;=&space;0&space;\\&space;\frac{\partial&space;\sum_{i=1}^{N}\frac{1}{2}&space;y_{i}-f(x_{i})}{\partial&space;b}&space;=&space;\frac{\partial&space;\sum_{i=1}^{N}\frac{1}{2}y_{i}-f(x_{i})}{\partial&space;b}&space;=&space;\sum_{i=1}^{N}&space;(y_{i}-a-bx_{i})(-x_{i})&space;=&space;0">



・1/2をしていない場合
<img
src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;\sum_{i=1}^{N}&space;y_{i}-f(x_{i})}{\partial&space;a}&space;=&space;\frac{\partial&space;\sum_{i=1}^{N}2&space;(y_{i}-f(x_{i}))}{\partial&space;a}\\&space;=&space;\sum_{i=1}^{N}&space;2(y_{i}-a-bx_{i})(-1)&space;=&space;0&space;\\&space;\leftrightarrow&space;\sum_{i=1}^{N}&space;(y_{i}-a-bx_{i})(-1)&space;=&space;0&space;\\&space;\\&space;\frac{\partial&space;\sum_{i=1}^{N}2(y_{i}-f(x_{i}))}{\partial&space;b}&space;=&space;\frac{\partial&space;\sum_{i=1}^{N}2(y_{i}-f(x_{i}))}{\partial&space;b}&space;\\=&space;\sum_{i=1}^{N}2&space;(y_{i}-a-bx_{i})(-x_{i})&space;=&space;0&space;\\&space;\leftrightarrow&space;\sum_{i=1}^{N}&space;(y_{i}-a-bx_{i})(-x_{i})&space;=&space;0">

と結局は1/2をしようがしまいが,最終的に同じ式を計算することには変わりません。
これは
<img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;E}{\partial&space;a}">や
<img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;E}{\partial&space;b}">自体が大事なのではなく、
<img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;E}{\partial&space;a}&space;=&space;0,\frac{\partial&space;E}{\partial&space;b}=0">
という方程式がここでは大事だからです。 これが最初の質問でもある「計算簡略化のために2乗する」ということにも繋がっています。重要なのはE自体の式ではなく、Eを最小化するaとbを求めることです。

この微分（偏微分）した後の係数をなくすために先にその係数を1にする（今の場合は2×1/2）という作業は、関数を最適化するラグランジュの未定乗数法を用いた分野では特によく用いられている計算簡略化のためのテクニックです。
SVM（サポートベクターマシン）やナイーブベイズや誤差逆伝搬学習法でもみられる方法ですので、これも覚えておくとそれらを理解するときにスムーズにいけると思います。
