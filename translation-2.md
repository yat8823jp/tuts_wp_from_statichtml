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

このシリーズの過程で、テーマがウィジェットを内包出来るようにするには、メニューやループを