○環境　PlayOnLinux 4.2.12　Ubuntu 18.04
（当該ファイルの場所）
エラーの発生場所　/usr/share/playonlinux/python/lib/lng.py　が参照するファイル（pol.mo）のエラー
エラーが発生する原因　/usr/share/locale/ja/pol.mo　の中のコード記載ミス。
★pol.moファイルは、MintのバージョンやPlayOnLinuxのバージョンなどの状況によって、
フォルダの場所が変わりますので、ファイルシステム内で、pol.moを検索して見つけます。
jaとあるフォルダーの中にあるはずです。検索で出たフアイルを右クリック＞Open folder（フォルダを開く）。

Linux Mint では、　
/usr/share/locale/ja/LC_MESSAGES/pol.mo

 PlayOnLinux 4.3.4では、　
/usr/share/playonlinux/lang/locale/ja/LC_MESSAGES/pol.mo
にありました。　

（対策のとり方）
○原因
pol.mo　の中の　497行？あたりの
msgstr "{0 }をリフレッシュ中"　を
msgstr "{0}をリフレッシュ中"　と修正する。（0の後ろのスペースを削除する。）

○修正方法
pol.moファイルを、Downloadの中にpol-moなどのフォルダを作ってその中にドラッグでコピーしておく。
moファイルはバイナリなので、これを編集可能なpoに変換してから修正し、
そのpoをmoに逆変換して、そのファイルを置き換える。

○mo-po 変換方法
.mo ファイルを .po ファイルに戻す方法 -Qitaの方法
　1.　オンラインサービス Online Tools for WordPress Developers を使う方法
https://ezgif.com/po-to-mo/ezgif-4-7b5d3188421c.po
http://tools.konstruktors.com/
ファイルを指定して変換ボタンを押すと変換ファイルが、Downloadフォルダに入る。

　2.　コマンドによる方法　
　　　msgunfmt [moファイルパス] -o [poファイルパス]
　　　msgfmt [poファイルパス] -o [moファイルパス]
テストフォルダにあります。
 ーー$msgunfmt ./beforepol.mo -o ./afterpolmo.pol
497行目
msgid "Refreshing {0}"
msgstr "{0 }をリフレッシュ中"
を
msgid "Refreshing {0}"
msgstr "{0}をリフレッシュ中"
に変更後
ーー$msgfmt ./afterpolmo.po -o ./pol.mo
このpol.moを使用する。

○修正したファイルの置き換え方法
そのままでは、置き換えが出来ません。
目的のフォルダーの空いている所を右クリック＞Rootとして開く＞パスワード入力＞
赤い権限昇格画面になる＞このフォルダに、修正ファイルをドラッグする＞更新日を確認する。

コマンドで行うときは、
$sudo mv /usr/share/playonlinux/lang/locale/ja/LC_MESSAGES/pol.mo /usr/share/playonlinux/lang/locale/ja/LC_MESSAGES/pol.mo.bk
$sudo ./pol.mo /usr/share/playonlinux/lang/locale/ja/LC_MESSAGES/pol.mo

（修正後のメモ）
修正後のpol.mo
を上書きします。

/usr/share/locale/ja/LC_MESSAGES/pol.mo
/usr/share/playonlinux/lang/locale/ja/LC_MESSAGES/pol.mo
のどちらかに存在するようです。
