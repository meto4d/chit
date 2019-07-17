# Chit － したらば掲示板をチャット風に使う対話的インターフェース

PeerCast Plays Urahaku の為に作ったRubyスクリプトです。

* 一行入力すると投稿します。

* スレッドタイトルをパターンで指定して投稿先を指定することができます。

* Readlineライブラリを使っているので bash と同じように快適な行編集をす
ることができます(入力した投稿文の履歴は `~/.config/chit/history` に保
存されます)。

* いわゆる「多重投稿」（投稿間隔が短すぎて投稿が失敗すること）になった
場合は、自動で時間を置いて再投稿します。

* 新着レスを自動で読み込みます。

## 使ってみる

	$ ruby chit.rb shitaraba:///game/48538/PeerCast*:postable,oldest

とすると `PeerCast Plays Urahaku その108> ` のようなプロンプトが出て、
レスが入力できるようになります。行頭で Ctrl+D を入力すると終了します。

ffi が存在しない旨のエラーメッセージが出て起動しなかった場合は (sudo)
`gem install ffi` でインストールしてください。

# インストール

PATH の通ったディレクトリに `chit.rb` へのシンボリック・リンクを作って
はいかがですか。例えば chit.rb が /home/user/chit/chit.rb にあるとする
と：

	$ sudo ln -s /home/user/chit/chit.rb /usr/local/bin/chit

## スレッド指定文字列の仕様

注意：スレッド番号は未実装です！

     スレッド指定文字列：
        [プロトコル]://[ホスト]/[掲示板]/[スレッドパターン]:[オプション]

     例えば shitaraba:///game/1234/ABC*:postable,oldest で game/1234 掲
     示板の スレッドタイトルが ABC で始まるスレッドの内、スレッドストッ
     プになっておらず一番古くから存在するものを選択する。

     [スレッドパターン]はワイルドカード ? * を含むことのできるスレッド
     タイトルか、あるいは、スレッド番号（スレッドが立てられた Unix Time
     である整数）。

     [オプション]は、以下の単語をコンマ区切りで並べたもの。
     * oldest (一番古くに立てられたスレッドを選択)
     * postable (スレッドストップになっていないスレッドを選択)
