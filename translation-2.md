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

##Populating the Header File
-ヘッダーファイルの移入-

header.phpにindex.html上部をコピーします。
index.htmlを開き、**DOCTYPE宣言**から**div class="main"**までを選択します。

`
<!-- add a class to the html tag if the site is being viewed in IE, to allow for any big fixes -->
<!--[if lt IE 8]><html class="ie7"><![endif]-->
<!--[if IE 8]><html class="ie8"><![endif]-->
<!--[if IE 9]><html class="ie9"><![endif]-->
<!--[if gt IE 9]><html><![endif]-->
<!--[if !IE]><html><![endif]-->
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>WordPress Theme Building - Creating a WordPress theme from static HTML</title>
    <link href="style.css" rel="stylesheet" media="all" type="text/css" />
    <header role="banner">
        <div class="site-name half left"><!-- site name and description  --></div>
        <div class="site-name half left">
            <h1 class="one-half-left" id="site-title"><a title="Creating a WordPress theme from static html - home" rel="home">WordPress Theme Building</a></h1>
            <h2 id="site-description">Creating a WordPress theme from static html</h2>
        </div>
         <!-- an aside in the header - this will be populated via a widget area later -->
        <aside class="header widget-area half right" role="complementary">
            <div class="widget-container">This will be a widget area in the header - address details (or anything else you like) goes here</div><!-- .widget-container -->
        </aside><!-- .half right -->
    </header><!-- header -->
 
    <!-- full width navigation menu - delete nav element if using top navigation -->
    <nav class="menu main"><?php /*  Allow screen readers / text browsers to skip the navigation menu and get right to the good stuff */ ?>
        <div class="skip-link screen-reader-text"><a title="Skip to content" href="#content">Skip to content</a></div>
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">Latest news</a></li>
            <li><a href="#">Featured articles</a></li>
        </ul>
    </nav><!-- .main -->
    <div class="main">'
`

このコードをコピーし、header.phpに貼り付け、保存します。

##Populating the Sidebar File
-サイドバーファイルの移入-

サイドバー用に同様の作業を行います。
index.htmlの**「aside class="sidebar"」**要素とその内部全てを選択します。

`
<!-- the sidebar - in WordPress this will be populated with widgets -->
<aside class="sidebar widget-area one-third right" role="complementary">
    <div class="widget-container">
        <h3 class="widget-title">A sidebar widget</h3>
        <p>This is a sidebar widget, in your WordPress theme you can set these up to display across your site.</p>
    </div><!-- .widget-container -->
    <div class="widget-container">
        <h3 class="widget-title">Another sidebar widget</h3>
        <p>A second sidebar widget, maybe you could use a plugin to display a social media feed, or simply list your most recent posts.</p>
    </div><!-- .widget-container -->
</aside>
`

sidebar.phpにコピーし、貼り付けて保存します。

##Populating the Footer File
-フッターファイルの移入-
footer.phpを移入するプロセスもヘッダー、サイドバーと同様です。
サイドバーの後を全てを選択します。

`
</div><!-- .main -->
<footer>
    <!-- the .fatfooter aside - I use this to enable a screen-wide background on the footer while still keeping the footer contents in line with the layout -->
    <aside class="fatfooter" role="complementary">
        <div class="first quarter left widget-area">
            <div class="widget-container">
                <h3 class="widget-title">First footer widget area</h3>
                <p>A widget area in the footer - use plugins and widgets to populate this.</p>
            </div><!-- .widget-container -->
        </div><!-- .first .widget-area -->
        <div class="second quarter widget-area">
            <div class="widget-container">
                <h3 class="widget-title">Second footer widget area</h3>
                <p>A widget area in the footer - use plugins and widgets to populate this.</p>
            </div><!-- .widget-container -->
        </div><!-- .second .widget-area -->
        <div class="third quarter widget-area">
            <div class="widget-container">
                <h3 class="widget-title">Third footer widget area</h3>
                <p>A widget area in the footer - use plugins and widgets to populate this.</p>
            </div><!-- .widget-container -->
        </div><!-- .third .widget-area -->
        <div class="fourth quarter right widget-area">
            <div class="widget-container">
                <h3 class="widget-title">Fourth footer widget area</h3>
                <p>A widget area in the footer - use plugins and widgets to populate this.</p>
            </div><!-- .widget-container -->
        </div><!-- .fourth .widget-area -->
    </aside><!-- #fatfooter -->
</footer>
`

fotter.phpにコピー＆ペーストし、保存します。

main divのとじタグがサイドバーではなく、フッターで閉じられているのが何故か？と、不思議に思うかもしれませんが
後で設定したテンプレートファイルがサイドバーを持たない場合に、正しくdivタグが閉じられるためにです。


##Populating the Index File
-インデックスファイルの移入-

最後のステップはindex.phpファイルを設定することです。
これは少し複雑ですが、WordPressはヘッダー、サイドバー、フッターを含めて利用するために必要な、いくつかのPHPの機能を追加する必要があります。
空のindex.phpファイルを開き、以下のようにコードを追加します。

`
<?php get_header(); ?>
 
<?php get_sidebar(); ?>
<?php get_footer(); ?>
`

ヘッダーとサイドバーの間にスペースを開けて下さい。
もう一度index.htmlを開き、**div class="main"**の要素とサイドバーの間のコードを全て選択します。

`
<div class="two-thirds" id="content">
    <article class="post" id="01">
        <h2 class="entry-title">This is the title of a post or page</h2>
        <img class="size-large" alt="" src="images/featured-image.jpg" />
        <section class="entry-meta">
            <p>Posted on 5 November by Rachel McCollin</p>
        </section><!-- .entry-meta -->
        <section class="entry-content">
            <p>This is the content of the post. On an archive page it might be an excerpt of the post or you might include the entire content.</p>
            <h3>Images in WordPress</h3>
            <img class="alignright" alt="" src="images/another-image.jpg" />
            <p>This post has some images included - once you've converted this html to a WordPress theme you'll be able to get WordPress to handle images for you and life will be so much easier!</p>
 
            <p>It also has a featured image - again, WordPress will handle these for you and you'll never go back to static html again. You'll learn how to add support for featured images to your theme in Part 10 of this series. You can use them to automatically display images in your individual posts and pages and in archive pages, you'll learn how to set up a custom archive page in Part 11.</p>
        </section><!-- .entry-content -->
        <section class="entry-meta">
            <h3>Post Categories and Tags</h3>
            <p>In this section you can display information about the categories and tags associated with your post, you'll learn how to do this using WordPress template tags in Part 4 of this series.</p>
        </section><!-- .entry-meta -->
    </article><!-- #01-->
</div><!-- #content-->
`

これをコピーして、index.phpファイルのget_header()の行の下に貼り付け保存します。

##Summary
-要約-

これでWordPressテーマの初期設定ができました。
次のパートでは、テーマを動作させるためにスタイルシートを編集する方法を説明します。