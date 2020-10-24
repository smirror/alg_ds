# アルゴリズムとデータ構造
## 目的

このレポジトリは個人的なアルゴリズムとデータ構造に関する考え方をまとめたものです。

## 方針

方針としては、理論的目的や抽象的実装に関しては一般的なアルゴリズムとデータ構造の本に任せるとし、アルゴリズムやデータ構造を実用的に利用するためにはどのように問題を捕らえてアプローチし、問題解決を行うためにはどのように理想・抽象的なデータ構造やアルゴリズムを書き換えるかといった部分に焦点を当てたいと思います。

これを書くモチベーションとしては以下の二つの理由があります。

- 大学で教わるアルゴリズムとデータ構造は、理想的な(言ってしまえば綺麗で簡潔ななデータ)を扱っていたように感じます。しかし、講義の内容と時間的な制約から実装で終わり、学んだアルゴリズムがどのような問題に利用できるか、現実的な問題に落とし込むところまでは行われることは少なく、こうした講義で学ぶアルゴリズムやデータ構造のパワフルさをイマイチ理解されないというギャップがあるように思います。
- 一方、幸運なことに学生が競技プログラミングなどで学んだアルゴリズムやデータ構造を使う機会があったとしても、理論と問題に合わせた実装の間には小さすぎない溝があるように思います。具体例として[深さ優先探索を利用した問題](https://drken1215.hatenablog.com/entry/2020/05/04/190252)を解く場合、問題に適した再帰関数の構造は問題ごとに異なります。問題にあった変更箇所はある程度決まっていますが、普通の講義ではこうしたデザインに関わる内容は話されませんし、こうした内容が必要と感じるのはやはりアルゴリズムを実際に使う機会が多くなったときです。

各章ごとにアルゴリズムを紹介し、ライブラリを作成していきます。この段階でどうアルゴリズムを再利用できる形でデザインするかを重視し、実際に作成したかを説明します。

本レポジトリの内容が一番だとは思っていません。よりよいものがあったり、作成できたのであれば issue や Pull request など大歓迎です。

## 本レポジトリの実行環境
- Windows 10
  - Visual Studio Code
- WSL2
- Python3.8.5 64-bit

   [dev-packages]
    - autopep8 = "*"
    - flake8 = "*"

    [packages]
   - numpy = "*"
   - scipy = "*"
   - networkx = "*"
   - scikit-learn = "*"
   - numba = "*"
   - pythran = "*"




## 目次

- [オブジェクト指向](オブジェクト指向.md)



## 参考資料
