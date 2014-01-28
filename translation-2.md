[http://wp.tutsplus.com/tutorials/theme-development/creating-a-wordpress-theme-from-static-html-creating-template-files/](http://wp.tutsplus.com/tutorials/theme-development/creating-a-wordpress-theme-from-static-html-creating-template-files/)

#Creating a WordPress Theme From Static HTML: Creating Template Files
-テンプレートファイルの作成：静的なHTMLからWordPressのテーマを作成する-

##What You’ll Need

このチュートリアルで必要なものは、HTMLやPHPを編集できる基本的なツールです。

* 好きなエディタ

##What Are Template Files?
-テンプレートファイルとは-

ワードプレスのテーマは、テンプレート·ファイルの数で構成されています。
それを動作させるために最低でも、index.phpをとstyle.css、この2つのファイルを含んでいる必要があります。

しかし、よく書かれたテーマに、index.phpファイルの内容がメインのテンプレートファイル（index.php）とインクルードファイルにセットされ、分割されています。
これらはサイドバーやフッターのコードを含むファイルです。

いくつかのテーマは、追加されたファイルを内包してループ処理されるように使用されています。
そのことについては、このチュートリアルではパート4で登場します。

それらのファイルの内容が内包されるようにWordPressに伝えるには、index.phpにそれらのファイルをインクルードするようにコードを書きます。

index.htmlを4つのphpファイルに分割します。

* index.php:メインコンテンツと他のファイルを内包するコードが含まれています。
* header.php:ヘッダーとナビゲーションに加え、&lt;head&gt;セクションが含まれます。
* sidebar.php:サイドバーのウィジェット領域が含まれます。
* footer.php:フッターに加え、終了の&lt;/body&gt;タグを含みます。

このシリーズの過程で、テーマのウィジェットがメニューやループで内包出来るようにする為、これらのファイルに追加し、更に、プラグインが利用するフックを追加します。
また、様々な種類のコンテンツを表示するため、必要なテンプレートファイルを追加します。
これらを行う上で、有利に始めたい場合は、WordPress Codexの「[Template Hierarchy(http://codex.wordpress.org/Template_Hierarchy)]」を参照して下さい。

しかし、現在やろうとしていることは、index.phpファイルの内容を分割し、PHPファイルのセットを作成することです。

##Creating PHP Files
-PHPファイルを作る-

最初のステップは、空のファイルを作成することです。次の4つの名前のファイルを作成し、エディタで開いて下さい。

* index.php
* header.php
* sidebar.php
* footer.php

これらの全てのファイルがテーマフォルダに入っていることを確認して下さい。テーマフォルダの名前は「wptutsplus-demo-theme」とします。

また、このフォルダにスタイルシートをコピーします。このチュートリアルでは編集しませんが、シリーズの次の項目ですることになります。