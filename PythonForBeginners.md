# 初めに


# データ構造

## BFS
[D. Ki](https://atcoder.jp/contests/abc138/tasks/abc138_d)
```python
import sys
from collections import deque


def bfs(N, G, P):
    dist = [-1]*N
    que = deque([0])
    dist[0] = 0
    while que:
        v = que.popleft()
        for w in G[v]:
            if dist[w]:
                que.append(w)
                P[w] += P[v]
                dist[w] = 0
    return P


def main():
    n, q = map(int, sys.stdin.buffer.readline().split())
    tree = [[] for i in range(n)]
    for _ in range(n-1):
        a, b = map(int, sys.stdin.buffer.readline().split())
        tree[a-1].append(b-1)
        tree[b-1].append(a-1)

    ans = [0]*n
    for a in sys.stdin.buffer.readlines():
        p, x = map(int, a.split())
        ans[p-1] += x

    print(*bfs(n, tree, ans))


if __name__ == "__main__":
    main()
```

## 木構造
 [k 番目に小さい値を取得可能な集合を管理するデータ構造](https://kazuma8128.hatenablog.com/entry/2018/06/20/210631)

### セグメント木
#### 双対セグメント木
- [双対セグメント木という概念について](https://kimiyuki.net/blog/2019/02/22/dual-segment-tree/)



# アルゴリズム
##  [格子点の数え上げの高速化](https://min-25.hatenablog.com/entry/2018/05/03/145505)

https://twitter.com/kyopro_friends/status/1304063876019793921?s=20

## 動的計画法(DP)
動的計画法は、ある問題に対し複数の問題に分割し、部分問題の計算結果を記録しながらと解くアルゴリズム全般を指します。

このとき、部分問題の結果を用いた結果と元の問題を解くことは同値であることが求められます。

### 桁DP
桁ごとに分けて考える動的計画法です。

- 非負整数 $X$ が $X≤K$ の範囲を動くときの、〜〜〜の最大値を求めよ
- 非負整数 $X$ が $X≤K$ の範囲を動くときの、〜〜〜という条件を満たすものは何通りあるか

という形式の問題が多いです。

与えられる$K$が大きいというのも特徴(というのも、桁毎に計算を行うため時間計算量としては$O(|K|\alpha)$となり非常に高速で計算できることが分かり、全探索では計算時間が膨大というケースが想定されます。逆に言えば、現実問題として何らかの条件にマッチするかを探索する場合、$10^6-10^7$程度の大きさで全探索で調べられるなら、全探索するのが他者からコードの意図が読みやすく、バグを埋め込む可能性も低く安全とも言えます。

#### 実装方針

結論ですが，桁 DP は以下の方針に従うとほぼ機械的に書け，バグりにくいと思います:

-「配る DP」で書く
-「遷移前の状態」「状態遷移」「遷移後の状態」を変数で管理し，遷移前の状態と状態遷移の列挙を全て `for` 文に任せる
- `for` 文の中では，まず遷移後の状態を表す変数を遷移前の状態で初期化し，必要に応じて遷移後の状態を書き換える
- 不要な遷移は `continue` で抜ける



この実装方針だと、`+=`  や `chmax` を含む「遷移式」を 1 本しか書かずに済み，コードが簡潔になります．

以下では例題とともに実装を紹介します．全て 0-indexed に統一して書きます．

#### 参考
- [桁 DP の思想 〜 K 以下の整数を走査するとはどういうことか 〜](https://drken1215.hatenablog.com/entry/2019/02/04/013700)

- [ Digit DP 入門](https://torus711.hatenablog.com/entry/20150423/1429794075)

- [桁DP入門](https://web.archive.org/web/20190103133620/https://pekempey.hatenablog.com/entry/2015/12/09/000603)
- 
-[ 桁 DP の簡潔な実装](https://opt-cp.com/digit-dp-implementation/)



# 実装テクニック

## 二項係数
- [よくやる二項係数 (nCk mod. p)、逆元 (a^-1 mod. p) の求め方](https://drken1215.hatenablog.com/entry/2018/06/08/210000)


# 数理最適化

## マッチング

- [重み付きマッチング概観](https://ygussany.hatenablog.com/entry/2020/12/03/000000)


## オンライン最適化
### von Neumannのミニマックス定理
- [Blackwellの接近可能性定理](https://tasusu.hatenablog.com/entry/2020/12/20/182721)

# 参考文献
## Python
1. [Python関連記事まとめ](https://note.nkmk.me/python-post-summary/#docstring)
   - 日本語で書かれたPython文法記事ではダントツでこれを読むべき。サムライやテックアカデミーを避けたいときはこちらから検索した方が良い
   - Qiitaにも良い記事はたくさんあるが、これだけ網羅的にまとめられているのはこれぐらいと思っています。
2. [AtCoderで始めるPython入門](https://qiita.com/KoyanagiHitoshi/items/3286fbc65d56dd67737c)
   - @KoyanagiHitoshi による記事。
   - こちらの記事も競プロに限定しているとは言え、Pythonを書いたことがなければこちらから進めるのはおすすめ。
2. [AtCoderの問題を分類しました](https://qiita.com/KoyanagiHitoshi/items/32dc42d8c5ee75339e54)
   - @KoyanagiHitoshi による、更に色々と勉強したい人向け。
   - これを空で書ければ、Pythonの知識に関してはそこそこだと思います(逆を言えばここからが、差の付け所)
4. [python 組み込み関数を全て(69個)紹介する](https://qiita.com/anieca/items/5afa1787aa0c7cd3ab49)
   - Pythonにデフォルトで使える関数の説明。
   - よく使うものから全く使ったことがないものまで紹介してあるので一読して良いと思います

5. [The Little Book of Python Anti-Patterns](https://docs.quantifiedcode.com/python-anti-patterns/index.html)(アンチパターン集)
6. [Green Tea Press](https://greenteapress.com/wp/)

### ライブラリ
1. [Pythonで競技プログラミング -ライブラリ編-](https://qiita.com/Kentaro_okumura/items/5b95b767a2e691cd5482)
    - 基本ライブラリの中で(競プロでは)よく使う関数と書き方を纏めた記事です。
    - これだけでも知っている人はPython書けると言っている人の中でも少な目と思ってます。
2. [Pythonで競プロするのに必要な機能をまとめてみた~itertools~](https://qiita.com/DaikiSuyama/items/11f63a94d63fa72e8bf4)
   - itertools に関する記事。これぐらいまとまっていると読み応えも、学びもあります。
3. [Awesome Python：素晴らしい Python フレームワーク・ライブラリ・ソフトウェア・リソースの数々](https://qiita.com/hatai/items/34c91d4ee0b54bd7cb8b)
   - ライブラリ集。こんなにあるんですね

### Numpy
1. [100 numpy exercises](https://github.com/rougier/numpy-100)
   - 有名だけど別に一から詳しく説明しくれるわけでもないので、そこまで良いとは思わない。
   - 答えのファイルを眺めてこんな書き方が出来るのだな、とNumpyに慣れるのが正解と思っている
2. [From Python to Numpy](https://www.labri.fr/perso/nrougier/from-python-to-numpy/)

### Scipy
1. [Elegant SciPy](https://github.com/elegant-scipy/elegant-scipy)

### Pandas
1. [Python初学者のためのPandas100本ノック](https://qiita.com/kunishou/items/bd5fad9a334f4f5be51c)
   - 解いたこともないので、良いのかはわかりませんがこういった教材もあります。

### Data Science 向けの本
1. [Python Data Science Handbook](https://github.com/jakevdp/PythonDataScienceHandbook)
2. [Statistical Thinking for the 21st Century](https://statsthinking21.org/)

### Webスクレイピング
1. [PythonでWebスクレイピングする時の知見をまとめておく](https://vaaaaaanquish.hatenablog.com/entry/2017/06/25/202924)
2. [Requests: 人間のためのHTTP](https://requests-docs-ja.readthedocs.io/en/latest/#)

## R
1. [R Cookbook, 2nd Edition](https://rc2e.com/)
3. [R for Data Science](https://r4ds.had.co.nz/)
4. [Advanced R](https://adv-r.hadley.nz/index.html)
5. [私たちのR: ベストプラクティスの探究](https://www.jaysong.net/RBook/)
6. [Doing Meta-Analysis in R ](https://github.com/MathiasHarrer/Doing-Meta-Analysis-in-R)

### パッケージ
1. [R Packages](https://r-pkgs.org/)
1. [Rのおすすめパッケージ2019年版](https://www.marketechlabo.com/r-best-packages/)

### ggplot2
5. [ggplot2: Elegant Graphics for Data Analysis](https://ggplot2-book.org/index.html)
