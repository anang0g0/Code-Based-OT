# Code-Based-OT

https://eprint.iacr.org/2007/382.pdf

https://en.wikipedia.org/wiki/Oblivious_transfer

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
