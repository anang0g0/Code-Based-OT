# Code-Based-OT



https://eprint.iacr.org/2007/382.pdf

https://en.wikipedia.org/wiki/Oblivious_transfer

# 20201122

https://www.nict.go.jp/publication/shuppan/kihou-journal/kihou-vol57no3_4/kihou-vol57no3-4_0403.pdf

 アリスが持つ２つのメッセージ$m_0,m_1$のどちらかをボブに送りたい。

ボブが秘密鍵と公開鍵のペア(g,H)を作成する。

更にボブはランダム線形符号H'を作る。

ボブは選択ビットb=(0,1) を選ぶ

ボブは2つの公開鍵(H,H')をアリスに送信する

b=0のとき$x_0=(H,H'),m_0$が欲しい。

b=1のとき$x_1=(H',H),m_1$が欲しい。

アリスはベクトルの対$x_b$ を受け取る。

アリスはメッセージm_0,m_1を選び、wt(e)=wt(e')=tのエラーベクトルを使って次のように暗号文を生成する。

```math
b=0 then

c_0=(h(e_0) \oplus m_0H) ,e_0H)

c_1=(h(e_1) \oplus m_1H') ,e_1H')

b=1 then

c_0=(h(e_0) \oplus m_0H') ,e_0H')

c_1=(h(e_1) \oplus m_1H) ,e_1H) 

```

アリスは2つの暗号文$(c_0,c_1)$をボブに送り返す。

ボブは$c_0,c_1$の片方$c_b$を復号して情報$m_b$を得る。

ここで、ボブは$m_b$のどちらか片方しか復号できません。

なぜなら片方はランダム線形符号だからです。


つまり、アリスが送信した2つの情報のうち片方しか受け取ることができないため、

受け取ることができなかった方の情報を知ることはありません。


以下の方式は完全にやぶられることが分った。なので既存の方式を符号で真似してみることにした。

# 20201121

https://qiita.com/fumumue/items/1849e283dc213a6f55f6

一般化してみました。

# 20201118

英語版ウィキの忘却転送によるメッセージ選択を、ニーダーライターで実現できるという確証が得られたので実装することにする。

[OEAP的ニーダーライター暗号化を用いた忘却転送プロトコル]　　（その１）

１．アリスはメッセージm0,m1を持っている。そこでボブに２つの乱数x0H,x1Hを送る。
ここでＨはアリスの公開鍵、x0,x1はアリスの秘密のエラーベクトル、x0H,x1Hは公開シンドロームである。

２．ボブは秘密の乱数ｋとランダムエラーeとそのハッシュ値h(e)、秘密のビットb=(0,1)を選び、次のようにアリスの公開鍵で暗号化しアリスに暗号文ｖを送る。

v=(h(e)^(xbH^kH),eH)、ここでwt(x0)=wt(x1)=wt(k)=t/2,wt(e)=tである。

アリスがボブからのメッセージの復号に失敗したら、成功するまでやり直す。

３．アリスはvを復号して(xb^k)を取り出し、次を計算する。ここでhはハッシュ関数である。

ここでkはアリスにとって知られない必要がある。

k0 = h(xb^x0^k)

k1 = h(xb^x1^k)

アリスはこの時、ボブの秘密ｋを見ているが、bが秘密なのでどちらが正しいｋなのか判別できない。（x0^x1^kを見ているのかもしれない）
そしてアリスは次のようにメッセージmb'を送る。

m0'=m0^k0 = m0^h(xb^k^x0)

m1'=m1^k1 = m1^h(xb^k^x1)

４．ボブは選択したビットbを使って平文mbを得る。

mb=mb'^h(k)

bはボブの秘密なので、アリスはm0,m1のどちらのメッセージをボブが復元したのかわからない。
また、ボブはアリスの秘密のエラーベクトルx0,x1を知らないので、ハッシュ値から残りのメッセージm_{b^1}を知ることができない。

（エラーベクトルの重みが必ずしもtにならないことが惜しいところ、改良します）



# 20201117

なかなかOTを何に使えるのか具体的に説明できなかったのですが、
この英語のウィキの説明と論文を読んで、自分で具体例を作って計算したら理解できました。
どうしてどの本もウィキみたいな解りやすい具体例を使って説明しないんだろうとちょっと疑問に思いました。
本代返せｗ。

ウィキにある例を符号でやってみようと思います。（デジタル署名とほとんど変わらない）
私の理解は怪しいですが、先行研究が既にあるので真似はできるものだと思います。

この英語の説明を読んで解るのは、２つの秘密のうち相手がどちらを復号したのかは送信者にはわからず、
受信者は自分の選んだビットに相当する秘密を手に入れるだけで、送信者の持っているもう一つの秘密については知ることができないということです。
非常に回りくどいですが、互いに相手が何を選んだかを知られたくない場合に使えるというものです。
つまり複数の選択肢の中で、相手の選択に関する情報（何の情報を持っているか、何を選んだか）が秘密に守られるということです。

情報屋が取引に使いそうですねｗ。

マルチパーティープロトコルや秘密計算について使われているらしいですが、もっと身近にプライベートな使い方をしてみたいです。
