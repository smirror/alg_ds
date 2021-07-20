---
title: "オブジェクト指向の意味"
tags: ""
---
- [1. 要諦](#1-要諦)
- [2. オブジェクト前史](#2-オブジェクト前史)
  - [2.1. ソフトウェア危機(1968-72)](#21-ソフトウェア危機1968-72)
  - [2.2. 構造化プログラミング(1969-75)](#22-構造化プログラミング1969-75)
- [3. Smalltalkとオブジェクト指向の誕生（1972 - 81）](#3-smalltalkとオブジェクト指向の誕生1972---81)
- [4. オブジェクト指向](#4-オブジェクト指向)
  - [4.1. C++(1979-88)](#41-c1979-88)
- [5. ソフトウェア開発方法論からみたオブジェクト指向](#5-ソフトウェア開発方法論からみたオブジェクト指向)
- [6. 先進的オブジェクト言語](#6-先進的オブジェクト言語)
  - [6.1. GO](#61-go)
  - [6.2. Rust](#62-rust)
- [7. 参考資料](#7-参考資料)
- [8. おまけ](#8-おまけ)

# 1. 要諦
最近のオブジェクト指向言語(といって良いのかは分かりませんが)GoやRustではClassが使われないと聞いて、最近の言語はどのようにオブジェクト指向を捉え（そして反省し）実装されているのだろうと気になったのが発端です。

この記事は***自分のために***纏めたものなので、詳細に関して往々に間違っている部分もあると思われますが、見つけた場合は教えてくださるとありがたいです。

# 2. オブジェクト前史
## 2.1. ソフトウェア危機(1968-72)
この時代とは、コンピュータの急激な高性能化によって、従来のようにアセンブラや機械語でプログラミングする時代から、（現在からしたら低級言語に近いとは言え)FORTRANやCOBOL, BASICといった高級言語（かつ非構造言語）が登場したことと
ハード・ソフトの技術の進歩に伴うコンピュータ上のシステムが扱う問題が益々複雑化することによる影響を表したものである。


>（ソフトウェア危機の主たる原因は）マシンがますます強力になってきたことだ！ はっきり言ってしまえば、マシンさえなければプログラミングには何の問題もない。貧弱なコンピュータが数台あるだけだったなら、プログラミングは穏やかな問題になる。しかし現在の我々は強大なコンピュータを所有しているため、プログラミングも同様に強大な問題となっているのだ。—Edsger Dijkstra、The Humble Programmer (EWD340)、Communications of the ACM

実際に開発者側の視線から見た当時のソフトウェア開発の実態は、フレデリック・ブルックスの『人月の神話(The Mythical Man-Month: Essays on Software Engineering)』が、詳細にその時代の問題点を考察している。

特に実際の開発プロジェクトでは
- 予定期間を超過してしまったプロジェクト
- 品質の低いソフトウェア
- 要求仕様を満たさないソフトウェア
- 管理不能状態のプロジェクトと、保守困難となったコード

として現れた。(そして現在の開発においても同様の問題はある)

勿論、Simulaといった現在主流に使われているオブジェクト指向言語のひな形は既に存在していたが、これらの言語は主に物理シュミレーションへの利用に限られており、研究目的であったことは明白だ。
しかしSimulaが研究目的であったとは言え、現在よく使われているPythonといったオブジェクト指向言語に影響を与えたSmalltalkはSimulaから多大な影響を受けており、現在のオブジェクト指向の特徴を広げたC++もSimulaの影響を強く受けていた。


## 2.2. 構造化プログラミング(1969-75)
ソフトウェア危機問題が計算機科学分野全般で取り沙汰されことで、エドガー・ダイクストラは、1968年にACM(Association for Computing Machinery)機関誌への投書 [Dijkstra, Edsger W. A Case against the GO TO Statement (EWD-215). E.W. Dijkstra Archive. Center for American History, University of Texas at Austin [EDM68] ](http://www.cs.utexas.edu/users/EWD/ewd02xx/EWD215.PDF)
(Go To Statement Considered Harmfulとも言われている)でgoto文利用の問題を指摘し、1989年にNATOソフトウェア工学会で[E. W. Dijkstra, “Structured Programming”, In Software Engineering Techniques, B. Randell and J.N. Buxton, (Eds.), NATO Scientific Affairs Division, Brussels, Belgium, 1970, pp. 84–88. [EDM69] ](http://homepages.cs.ncl.ac.uk/brian.randell/NATO/nato1969.PDF)を発表した。

構造化プログラミングはコンピュータプログラムの明瞭化を目的にした手法であり、一般的には順接、分岐、反復の三つの制御構造（control structures）によって、処理の流れを記述することであると認識されている。更にコードブロックとサブルーチンも加えられることがある。

1. **順次**（sequence）サブプログラムを順々に実行する。`文1; 文2`
2. **選択**（selection） 条件式が導出した状態に従い、次に実行するサブプログラムを選択して分岐する。`if 式 then 文1 else 文2 fi`
3. **反復**（repetition）条件式が導出した特定の状態の間、サブプログラムを繰り返し実行する。`do 文 od`
4. **サブルーチン**（subroutine）一定量の命令コードを任意の定義名で抽象化し、その実装内容を分離したものである。ブロックとサブルーチンは相互再帰の関係にある。ブロックの中のステートメントからサブルーチンが呼び出され、そのサブルーチンの中にもまたブロックとステートメントがあるといった具合である。サブルーチンはその終点に達すると復帰（return）されて、呼び出したステートメントの次の行に制御が移る。また終点前の任意の位置でも復帰できる。

よく知られている構造化プログラミングは[EDM68]の内容が元になっているが、同時期に発表された[EDM69]と混同され。，名称が取り違えられ現在に至っている。


[EDM68] の趣旨は次の通りになる：
- 人間が時間によって変化するプロセスを把握する能力は、プログラムの静的な関係を把握する能力に比べて劣っているため、静的なプログラムテキストの構造と時間によって変化するプロセスの構造をなるべく近づけるのが重要である。
- そのためにはプロセスの進捗を表す簡潔な指標が必要である。指標とは例えば実行中の行番号・その時点でのスタックトレース・行番号とループを回った回数のペアなどである。
- 例えば、1人が部屋に入るごとにカウンタを増やしていくプログラムにおいて、カウンタが室内の人数-1である瞬間はどこにあるのかという問いに答える際に、簡潔な指標があればすぐ答えられるが、簡潔な指標がなければ正確な答えは難しくなる。
- goto文を無条件に許してしまうと簡潔な指標は得られなくなってしまうため、高水準プログラミング言語においてはgoto文は廃止するべきである。

[EDM69]では、プログラム正当性の効率的な検証技術に重点を置き、当時問題視されていたコードサイズの際限なき肥大化によるソフトウェア危機の解決策として従来のボトムアップ設計からトップダウン設計への移行を推奨していた。
要旨は以下の通りである:
- **良く構造化されたプログラム(well-structured programs)**:プログラムサイズの肥大化に伴い、各プログラム部品およびそれらを組み合わせた際のプログラムの正当性の立証に必要な労力が指数的に増加して完遂が不可能になるというソフトウェア危機の問題に対して、プログラムの大きさによらない正しさを人間が確認できる構造にする。
- **段階的抽象化(step-wise abstraction)**:プログラムの意味のある部分をくくり出して抽象化文にすること。抽象化文は現在で言えば、関数やメソッドに相当し、これによってプログラムの可読性が向上する。ダイクストラは段階的抽象化をするプログラムは**構造化定理**と同様の**制御構造**(control structures）を使うべきと述べている。現代的にはボトムアップ設計にあたる。
- **段階的詳細化(step-wise refinement)**:詳細なプログラムを**抽象化**(abstraction）していくのではなく、逆に抽象的なプログラムから始めて**詳細化**(refinement）していくトップダウン設計も提案された。
- **抽象データとその上で動作する抽象化文の共同詳細化(joint refinement)**:抽象データ構造の詳細化とそれを扱う抽象ステートメントを同時に詳細化し、それを1つのプログラムのユニットに分離するというものである。これは現在のオブジェクト指向のクラスに近い発想であり、このユニットをダイクストラは真珠(pearl)と呼んだ。
- **プログラムの階層化**:抽象的な真珠が1段階具体的な真珠に依存し、その真珠がさらに具体的な真珠に依存していったものをネックレスに例えた。そしてネックレスの上部は下部に関わらず正しさを証明することができ、また下部を取り替えることでプログラムのバリエーションを労力をかけずに作れるとした。これは現在のオブジェクト指向の継承概念にあたる。

その一方でクヌースの指摘[Knuth, D. E. (1974). “Structured Programming with go to Statements Computing Surveys”. ACM, New York, NY, USA 6 (4): 261-301.[KDE74] ](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.103.6084)によると、ダイクストラは[EDM69]においてはgoto文には触れていない。実際に“sequencing should be controlled by alternative, condtional and repetitive clauses and procedure calls, rather than by statements transferring control to labelled points.[EDM69]”との1文があるのみでそれ以外では触れていない。

また、“I do not claim that the clauses mentioned are exhaustive in the sense that they will satisfy all needs[EDM68]”とし、「3つの基本構造」には固執していない。

「構造化プログラミングの観点からgoto文を使うのは望ましくない」ものの「単にgoto文を使わなければ見通しが良くなる」という考えは[EDM68]でも否定しており、goto文の有無のみに固執するのは問題を見誤っている。構造化プログラミングの本質の一つは、状態遷移の適切な表現方法とタイミングを見極めることである[A Method of Programming. E.W. Dijkstra, W.H.J. Feijen, trsl. by J. Sterringa. Addison Wesley. 1988.]。

# 3. Smalltalkとオブジェクト指向の誕生（1972 - 81）

まだ「オブジェクト指向言語」という言葉が無い1960年代に、Simulaというプログラム言語は現代でいうオブジェクト、クラス（抽象データ型）、動的ディスパッチ、継承、更にガーベジコレクトまで実装されていた。

この言語から、オブジェクトと「メッセージ」というプログラム概念のコンセプトに据え、プログラム内のあらゆる要素をオブジェクトとして扱い、オブジェクトはメッセージの送受信でコミュニケーションするという独特のプログラム理論--オブジェクト指向をアラン・ケイは提唱し、Smalltlkというプログラミング言語を設計することになった。

メッセージとはプログラムコードとしても解釈できるデータ列のことであり、そのデータ列を評価（eval）することで新たなデータを導出できるという仕組みを意味していた。
オブジェクトが受け取ったメッセージは任意のタイミングで評価できるので非同期通信、単方向通信（送りっぱなし処理）をも可能にしていた。この発想の背景にはLISPの影響があった。

アラン・ケイ自身はメッセージ送信について以下のように語っている。

>    I thought of objects being like biological cells and/or individual computers on a network, only able to communicate with messages.（さながら生物の細胞、もしくはネットワーク上の銘々のコンピュータ、それらはただメッセージによって繋がり合う存在、僕はオブジェクトをそう考えている）— Alan Kay

> ... each object could have several algebras associated with it, and there could be families of these, and that these would be very very useful.（銘々のオブジェクトは自身に伴う幾つかの「代数」を持つ、またそれらの家族たちもいるかもしれない、それらは極めて有用になるだろう）— Alan Kay

>The Japanese have a small word - ma ... The key in making great and growable systems is much more to design how its modules communicate rather than what their internal properties and behaviors should be.（日本語には「間」という言葉がある・・・成長的なシステムを作る鍵とは内部の特徴と動作がどうあるべきかよりも、それらがどう繋がり合うかをデザインする事なんだ）— Alan Kay

> I realized that the cell/whole-computer metaphor would get rid of data, ...（僕はこう気付いた、細胞であり全体でもあるコンピュータメタファーはデータを除去するであろうと、）— Alan Kay

>... there were two main paths that were catalysed by Simula. The early one (just by accident) was the bio/net non-data-procedure route that I took. The other one, which came a little later as an object of study was abstract data types, and this got much more play.（Simulaを触媒にした二本の道筋があった。初めの一本はバイオネットな非データ手法、僕が選んだ方だ。少し遅れたもう一本は抽象データ型、こっちの方がずっと賑わってるね。）— Alan Kay

当初は、Smalltalk を説明する中で、そのシステムが体現した「パーソナルコンピューティングに関わる全てを『オブジェクト』とそれらの間で交わされる『メッセージ送信』によって表現すること」を意味していた。

しかし現実には、データ列が常にコード候補として扱われる処理系は、当時のコンピュータには負荷が大きく実用的な速度を得られないという問題にすぐ直面した。Smalltalk-74とSmalltalk-76の過程で、やむなくメッセージはセレクタ仕様の追加と共に構想通りの評価ができないほどシステム向けに最適化され、レシーバーは動的ディスパッチとメソッド仕様が中心になり、オブジェクトはクラス定義の存在感が大きくなった。

>Smalltalk is not only NOT its syntax or the class library, it is not even about classes. I'm sorry that I long ago coined the term "objects" for this topic because it gets many people to focus on the lesser idea.The big idea is "messaging".（Smalltalkはその構文やライブラリやクラスをも関心にしていないという事だけではない。多くの人の関心を小さなアイディアに向かせたことから、僕はオブジェクトという用語を昔作り出したことを残念に思っている。大切なのはメッセージングなんだ。）— Alan Kay

1980年のSmalltalk-80は、元々はメッセージを重視していたケイを自嘲させるほど同期的で双方向的で手続き的なオブジェクト指向へと変貌していた。それでも動的ディスパッチと委譲でオブジェクトを連携させるスタイルは画期的であった。

Smalltalkの従来のプログラミング言語よりもOS概念が深く関わるような計算に関わる計算機全体を一つの集合体とみる独自の体系は、
最終的には当初の最低限のメッセージ送信を行う理想から外れた一方で、
ハードウェアリソースの制限や並列化が重要視された現代からすると、時代を先取りすぎた言語と言えるのではないだろうか？

メモリとCPUとそれに対する命令を持つ機械をさらに抽象化するとしたら、それは同じくデータと処理と命令セットをもつ仮想機械で抽象化されるべきだと考えていた。
これは、構造化プログラミングの中でダイクストラが仮想機械として階層的に抽象化すべきだと言っていたこととかぶる。

少なくとも昨今の言語で、Rustのメモリ所有権概念や
Goの並列化などでアラン・ケイが提唱したメッセージ送信と同等の概念が取り入れられ、重要視されているのは決して不思議なことではないように思える。

# 4. オブジェクト指向
## 4.1. C++(1979-88)
さて、Smalltalkは「オブジェクト概念」という言葉を作ったが、アラン・ケイの「オブジェクト概念」は最近まで伝わらなかった。
それは、Simulaの優れたコンセプトは他でも評価した言語が、現在でもよく使われているからだろう。

C++の作者であるビャーネ・ストロヴストルップは、オブジェクト指向を「『継承』機構と『多態性』を付加した『抽象データ型』のスーパーセット」（カプセル化、継承、多態性）と理解し、これが最近のオブジェクト指向の思想として広まった。

特にC++をきっかけに、オブジェクト指向の代表的な特徴と見なされたのが以下の三つの要素である：
- 継承
- ポリモーフィズム
- カプセル化

また以下の2点がSimula&C++の新たな言語特徴である：
- 動的ディスパッチ: 動的ディスパッチのキモは、オブジェクト自身が自分が何者であるか知っており、また、実行時に関数テーブルを探索して、どの関数を実行するかというところにある。SimulaもC++もvirtualという予約語を用いて、仮想関数の動的分配をすることを宣言できる。
- 継承と委譲:継承は、あるクラスの機能をもったまま、別の機能を追加したもう一つのクラスを作る仕組みだ。継承の代わりに委譲という手段を用いているプログラミング言語がある。これは、クラスベースのオブジェクト指向に対してプロトタイプベースのオブジェクト指向と呼ばれたりする。


1990年代までの(膾炙された)オブジェクト指向の要点は、以下五つに纏められる。：
- 抽象データ型：データと処理をひもづける
- 抽象データ型：情報の隠蔽を行うことができる
- オブジェクト：データ自身が何者か知っている
- 動的多態：オブジェクト自身のデータと処理を自動的に探索する
- 探索先の設定：継承、委譲




# 5. ソフトウェア開発方法論からみたオブジェクト指向
そもそも、オブジェクト指向なんて考えが出てきたきっかけはソフトウェア危機である。
しかし、私たちはオブジェクト指向を手に入れて、発端となった問題をクリアすることができたのだろうか--答えはNoだ。

- [関心の分離を意識した名前設計で巨大クラスを爆殺する](https://qiita.com/MinoDriven/items/37599172b2cd27c38a33)
- [責任(関心)を意識したアプリケーション設計](https://qiita.com/kamykn/items/3265ad2dfd91dc7e973f)
- [SOLID原則のまとめ](https://qiita.com/kkkkkou/items/ad5a7aeaee16bf55b3e2)
- [何かのときにすっと出したい、プログラミングに関する法則・原則一覧](https://qiita.com/hirokidaichi/items/d6c473d8011bd9330e63)


# 6. 先進的オブジェクト言語
他の言語や思想などの調査が必要なので仮。
とりあえずGOとRustは確実。

from: https://twitter.com/qnighy/status/1299698429086453760
RustとGoに共通して見られる脱クラス的設計 (以下他言語のclassをRust/Goのstructと対応づけて議論する)
・classから抽象化の機能を取り除いたこと (→Rustのtrait, Goのinterface)
・classからカプセル化境界の機能を取り除いたこと (→Rustのmodule, Goのpackage)
・グローバル関数の復権

- [ オブジェクト指向は失敗だった ](https://fj.hatenablog.jp/entry/2019/07/27/202138)
- [ オブジェクト指向プログラミング -- 1兆ドル規模の大失敗 ](https://okuranagaimo.blogspot.com/2019/07/1.html)
- [第2回勉強会 オブジェクト指向](https://www.slideshare.net/hakoika-itwg/2-14328264)
- [ オブジェクト指向についてそろそろ一席ぶっておく ](https://kbigwheel.hateblo.jp/entry/2018/09/28/053328)
- [ オブジェクト指向の原則集 ](http://tshix.hatenablog.com/entry/2016/03/29/020945)
- [【中級】基礎からのオブジェクト指向 第5部 「GRASPパターン」を理解する（前編）](https://xtech.nikkei.com/it/article/COLUMN/20060607/240196/)
- [オブジェクト指向の設計と実装の学び方のコツ](https://www.slideshare.net/masuda220/ss-14263541)
- [オブジェクト指向（導入）](http://teacher.nagano-nct.ac.jp/fujita/LightNEasy.php?page=Java_Intro)
- [9. オブジェクト指向](web.sfc.keio.ac.jp/~hattori/prog-theory/ja/9.html#id11)
- [オブジェクト指向はクソか？](http://tokoma1.hatenablog.com/entry/2015/06/07/083347)
- [その後のJoe Armstrongのオブジェクト指向に対する見解](http://tokoma1.hatenablog.com/entry/2015/06/07/083514)




## 6.1. GO
Go言語において、クラスは存在しない。その一方でメソッドは存在する。
メソッドは型に対して定義されるものであり、レシーバーを伴う関数を指す。
そのため、構造体以外の型に対しても、メソッドを宣言できる。
- [Goはオブジェクト指向言語だろうか？](https://postd.cc/is-go-object-oriented/)
- [Goでクリーンアーキテクチャを試す](https://postd.cc/golang-clean-archithecture/)
- [6年間におけるGoのベストプラクティス](https://postd.cc/go-best-practices-2016/)
- [なぜGo言語 (golang) はよい言語なのか・Goでプログラムを書くべき理由](https://www.yunabe.jp/docs/why_golang_is_good.html)
- [「Goの宣言構文について」を翻訳してみた](https://qiita.com/m0a/items/2b03b189d746ae231756)
- [Goは本当に1980年代の言語みたいなのか。](https://qiita.com/amaike/items/8105ed6ff69a61896e64)


## 6.2. Rust
オブジェクト指向的な書き方はできるけど、クラスがなくて代わりにimpl。

- [オブジェクト指向経験者のためのRust入門](https://qiita.com/nacika_ins/items/cf3782bd371da79def74)
- [Rustにおけるオブジェクト指向の考え方](https://qiita.com/mandel59/items/e9a5438f4c1d70cffb7a)
- [オブジェクト指向の錆](https://sodocumentation.net/ja/rust/topic/6737/%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E6%8C%87%E5%90%91%E3%81%AE%E9%8C%86)
- [Rustのオブジェクト指向プログラミング機能](https://doc.rust-jp.rs/book/second-edition/ch17-00-oop.html)
- [[翻訳] Python プログラマーのための Rust 入門](https://qiita.com/t2y/items/434854fab16159a7c0f7)
- [Rustに１００日触れてわかったこと](https://qiita.com/h1guchi/items/1f9b7e6367e8292f646f)
- [C++erのためのRust入門(未完)](https://qiita.com/EqualL2/items/a232ab0855f145bd5997)
- [Rustのメモリ管理って面白い](https://qiita.com/ksato9700/items/312be99d8264b553b193)
- [なぜRustを学ぶべきなのか 〜 5年経った今改めてまとめてみる](https://qiita.com/garkimasera/items/edce62f3fd6b2fe98d82)
- [Rustはこうやって勉強するといいんじゃないか、という一例](https://qiita.com/TakaakiFuruse/items/13e9ad9d1efe7e17811c)
- [Rustに影響を与えた言語たち](https://qiita.com/hinastory/items/e97d5459b9cda45758db#rust%E3%81%8C%E5%BD%B1%E9%9F%BF%E3%82%92%E5%8F%97%E3%81%91%E3%81%9F%E8%A8%80%E8%AA%9E)
- [Rustの概要や魅力をコードなしでまとめてみた]()
- [ Rustに影響を与えた言語たち ](https://hinastory.github.io/cats-cats-cats/2020/06/13/rust-influences/)
- [Rustでのモデル駆動設計について](https://creators-note.chatwork.com/entry/2020/12/23/000100)
# 7. 参考資料
- [新人プログラマに知っておいてもらいたい人類がオブジェクト指向を手に入れるまでの軌跡](https://qiita.com/hirokidaichi/items/591ad96ab12938878fe1#%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E6%8C%87%E5%90%91)
- [なぜオブジェクト指向は難しいのか](https://qiita.com/tutinoco/items/7f7568cc7dbf7e2276c8)
- [オブジェクト指向と10年戦ってわかったこと](https://qiita.com/tutinoco/items/6952b01e5fc38914ec4)

# 8. おまけ
- [ JuliaとLispのマクロの比較 ](https://muuuminsan.hatenablog.com/entry/2020/10/08/021903)
