[http://wp.tutsplus.com/tutorials/theme-development/creating-a-wordpress-theme-from-static-html-setting-up-the-header/](Creating a WordPress Theme From Static HTML: Setting Up the Header)

#Creating a WordPress Theme From Static HTML: Setting Up the Header
-ヘッダの設定：静的なHTMLからWordPressのテーマを作成する-

このシリーズは、これまでに静的なHTMLから基本的なテーマを作成する方法を次のように学んできました。

* WordPressのためのマークアップを準備
* HTMLをPHPに分割し、テンプレートファイルにしていく
* スタイルシートを編集し、WordPressのテーマにアップロードする
* indexファイルにループを追加する

このチュートリアルでは、パート2で作成したheader.phpファイルで作業します。

* <head>セクションにある既存の静的なメタタグを、自動的に生成されるよう置き換えます。
* WordPressの管理者権限を経由し、ユーザーがサイトのタイトルや概要を更新できるようにします。
* ヘッダーファイルにプラグインが使用するためのwp_headアクションフックを追加します。

##What You’ll Need
-必要なもの-

* エディタ
* ブラウザ 
* インストールされたWordPress （ローカルもしくはリモート）
* ローカルで作業する場合は、WordPressを実行するためのMAMP、WAMPまたはLAMPが必要です
* リモートで作業する場合はFTPのアクセス及び管理者アカウントが必要になります。


##1.ヘッダーファイルにメタタグを追加する

テーマに2つのメタタグを追加します。

###文字セットメタタグを更新する
書かれている業を検索する

```
<meta charset="utf-8" />
```
このように置き換えます

```
<meta charset="<?php bloginfo( 'charset' ); ?>" />
```

これで、文字セットのメタタグは、管理画面を介して設定されたものを自動的に使用します。

###タイトルタグを更新する

現時点では、テーマにはheader.phpファイルの中に次のコードを経由して追加された静的なタイトルタグがあります。

```
WordPress Theme Building - Creating a WordPress Theme from Static HTML
```

動的に生成されるタイトルタグを追加することで、WordPressが提供するSEOやユーザービリティ上の利点を与えるための追加機能を活用することが出来ます。

上記のコードを削除し、次のように置き換えます。

```
<?php
global $page, $paged;
wp_title( '|', true, 'right' );
// Add the blog name.
bloginfo( 'name' );
// Add the blog description for the home/front page.
$site_description = get_bloginfo( 'description', 'display' );
if ( $site_description && ( is_home() || is_front_page() ) )
    echo " | $site_description";
?>
```

このコードはいくつかのことを行います。

1.最初に使われているのは、ページタイトルのセパレータより右側に出力するテンプレートタグwp_title()です。
2.次は、テンプレートタグbloginfo()を利用し、パラメーター**name** を使用してサイト自体の名前を出力します。
3.訪問されたページがホームページならば（条件タグの**is_home（）| | is_front_page（）**を使用してチェックする）、テンプレートタグget_bloginfo()を使用し、サイトの説明を出力します。

ヘッダーファイルを保存する。

##Adding a Dynamically Generated Site Title and Description
-サイトのタイトルと説明を動的に生成するよう追加-

次のステップは、サイトのタイトルと説明を静的なものから動的なものへと置き換えることです。 
header.phpから次のコードを探します。

```
<div class="site-name half left"><!-- site name and description  --></div>
 
<div class="site-name half left">
    <h1 class="one-half-left" id="site-title"><a title="Creating a WordPress theme from static html - home" rel="home">WordPress Theme Building</a></h1>
    <h2 id="site-description">Creating a WordPress theme from static html</h2>
</div>
```

以下のコードに置き換ます。

```
<div class="site-name half left"><!-- site name and description  --></div>
 
<div class="site-name half left">
    <h1 id="site-title"></h1>
    <h2 id="site-description"></h2>
</div>
```

このコードは次のようになります。

* echo home_url()を利用し、サイトタイトルをホームページへのリンクでラップします。
* テンプレートタグbloginfo()の**name**パラメータを使用し、サイトのタイトルが表示されます。
* もういちどテンプレートタグbloginfo()をしようし、パラメータ**description**を利用してサイトの説明を表示します。

これで管理者の設定画面から、サイトのタイトルと説明を変更することができ、サイトのページすべてに反映されます
。

##テーマにwp_headアクションフックを追加する

wp_headアクションフックは、すべてのテーマに追加する不可欠なもので、header.phpファイルの&lt;/head&gt;タグの直後に置かれます。
プラグインがアクティブになっていても、テーマでそれを追加しなければ、サイトで動作しない場合があります。

サイトのfooter.phpファイルにあるwp_footerアクションフックが似ていて、このシリーズの8章で登場します。

&lt;/ head&gt;終了タグの前に、次のコードを追加します。

```
<?php wp_head(); ?>
```

ファイルを保存します。これで全て完了です。

##要約

全てのテーマファイルに含まれるべきである、header.phpファイルの幾つかの重要な要素を設定しました。

このシリーズの次の部分では、ヘッダーファイルにナビゲーションを追加する方法を学びます。その後、ヘッダにウィジェットを追加する方法を学び、連絡先の詳細を追加したりと、ヘッダに好きなものを載せれるようにします。

