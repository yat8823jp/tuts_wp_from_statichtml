[http://code.tutsplus.com/tutorials/creating-a-wordpress-theme-from-static-html-uploading-your-theme-to-wordpress--wp-33955](http://code.tutsplus.com/tutorials/creating-a-wordpress-theme-from-static-html-uploading-your-theme-to-wordpress--wp-33955)

#Creating a WordPress Theme From Static HTML: Uploading Your Theme to WordPress
-ワードプレスへテーマをアップロードする：静的なHTMLからWordPressのテーマを作成する-  

最初の２章では、静的なHTMLを用意して、WordPressで利用できるようにパーツ分けしていく方法を学びました。

これでテーマの初期的な設定はできましたが、このままでは、WordPressのテーマとして動かすことはできません。テーマを動かすためには、CSSに説明を記載し、WordPressがテーマを認識できるようにしないといけないので、その一連の作業をこの章でやってみようと思います。

その後、WordPressにテーマをアップロードし、テスト表示してみます。また、スクリーンショットを作成して、管理画面からテーマを選びやすいようにもします。

##What You’ll Need

これからWordPressで作業をするにあたって、下記のようなツールが必要になります。

* エディターツール（好きなものでOK）
* テスト表示用のブラウザ
* スクリーンショットを適切なサイズに編集できる画像編集ソフト
* WordPressがインストールされた環境（ローカルでもリモートでもOK）
* リモート環境を使う場合は、WordPressにアクセスするためのFTPのアカウント


##1.Setting Up the Theme in the Stylesheet
-スタイルシートにテーマの設定をする-

テーマをアップロードする前にスタイルシートを編集します。

テンプレートフォルダのstyle.cssを開き、その先頭に、下記のフォーマットに従ってテーマの情報を記載し、保存して閉じます。

```
/*
Theme Name: WordPress Theme Building from HTML - Part 3
Theme URI: http://rachelmccollin.co.uk
Author: Rachel McCollin
Author URI: http://rachelmccollin.co.uk
Description: The theme to accompany the wptutsplus series on creating a WordPress theme from static HTML. This theme accompanies Part 3 of the series.
Version: 3.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
*/
```

##2. Calling the Stylesheet From the Header File
-ヘッダーファイルからスタイルシートを読み込む-

いまheader.phpに記載されているスタイルシートのリンクは静的なリンクなので、WordPressでは読み込むことができません。そのため、テーマをアップロードする前に変更する必要があります。

header.phpファイルをあけて、下記の行を見つけて

```
<link href="style.css" rel="stylesheet" media="all" type="text/css" />
```

下記のように書き換えてください。

```
<link href="<?php bloginfo( 'stylesheet_url' ); ?>" rel="stylesheet" media="all" type="text/css" />
This includes the function <?php bloginfo( 'stylesheet_url' ); ?> 
```

これで、WordPressはCSSファイルを認識することができるようになります。その後、ファイルを保存して閉じてください。

##3.Creating a Screenshot
-スクリーンショットをつくる-

最後は、テーマのスクリーンショットの作成です。

スクリーンショットのサイズは横幅600px、縦450pxと決まっています。

ブラウザーからスクリーンショットを作成し、画像編集ソフトで適切なサイズに加工してください。私はいつもPhotoshopを使っています。

縦横の比率が12:9になるように画像をトリミングし、横600px、縦450pxのPNG形式のファイルにしてください。ファイル名はscreenshot.pngとし、テーマフォルダに保存します。

##4.Uploading Your Theme to WordPress
-テーマをWordPressにアップロードする-

次は、作成したテーマをWordPressにアップロードします。
もうすでにWordPressはインストール済みとは思いますが、もし方法がわからなければCodexを参照してください。

テーマをアップロードするには、２通りの方法があります。

1. FTP（もしくは、ローカル環境で構築したフォルダ）を使って、作成したテーマを複製し、wp-contentの中のthemesフォルダの中に保存します。
2. Zipを使う場合は、テーマ管理画面から、「テーマ ＞ 新規追加」を選択し、ファイルをアップロードします。

その後、テーマ編集画面を開くと、作成したテーマが表示されていると思います。そのテーマを選択して、有効化してください。

##5.Testing Your Theme
-テーマの確認をする-

ついに、テーマがきちんと動くかのチェックをするときがやってきました。
ウェブサイトにアクセスし、何が表示されているのかを見てみましょう。

私のウェブサイトは、このような感じになっています。

サイトを見てみると、画像が表示されていない事がわかります。それは、hrefの参照先が静的になっているため、WordPressが画像を認識できないからです。

ロゴや背景、コンテンツの中に貼ってある画像等、WordPressで画像を表示するためには、WordPressが、画像がどこにあるのかを認識できるようにしなくてはいけません。

コンテンツの中の画像が表示されなくても心配しなくてOKです、これは後で出てくる章の中で、WordPressのループを設定すれば、自動的に表示されるようになります。

##6.Updating Image Links in Template Files
-テーマファイルの画像リンクを修正する-

この章では、テンプレートファイルの中で画像を使っている場合についての説明になります。

コンテンツの中に使われている画像はループの設定をすれば表示されるようになりますが、テンプレートファイルではそれができないので、直接リンクを設定しないといけません。

例えば、ヘッダーの中にロゴがあるとします。そのリンクが下記のように書いてあった場合、

```
<img alt="" src="images/logo.jpg" />
```

もともと作っていた静的サイトでは、ブラウザーが相対パスで画像を読み込むことができるため、このような書き方をしていました。

ですが、WordPressでは同じ方法で表示することができません。代わりに、テーマの中に使われている画像が、テーマのサブフォルダに収納されていることを、WordPressが認識できるようにしないといけないのです。
そうするためには、header.phpをあけて、ソースコードを下記のように書き換えます。

```
<img alt="" src="<?php bloginfo( 'stylesheet_url' ); ?>/images/logo.jpg" />
```

そう、ここに出てきたPHPのコードは、さっきCSSを呼び出すときにつかったものと同じものですね。
ファイルを保存して、ブラウザを更新しましょう。テーマの画像が表示されていると思います。

##Summary
-まとめ-

ようやく、ほぼ、きちんと動くという段階のテーマまで近づいてきました。

WordPressでテーマを認識できるようにCSSの設定をし、ヘッダーテンプレートから呼び出せるようにリンクの設定をしました。また、テンプレートファイルから画像が読み込めるようにもしました。

次のチュートリアルでは、ループの設定の仕方をお伝えします。これは、WordPressで投稿や固定ページのコンテンツを表示するときに必要になるものです。
