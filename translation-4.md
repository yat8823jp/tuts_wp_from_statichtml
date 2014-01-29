[http://wp.tutsplus.com/tutorials/theme-development/creating-a-wordpress-theme-from-static-html-adding-a-loop/](http://wp.tutsplus.com/tutorials/theme-development/creating-a-wordpress-theme-from-static-html-adding-a-loop/)

#Creating a WordPress Theme From Static HTML: Adding a Loop
-ループの追加：静的なHTMLからWordPressのテーマを作成する-

シリーズ最初の3ステップでは、WordPressのために静的なHTMLを用意し、htmlファイルをテンプレートファイルのセットに分割、し、スタイルシートを編集してテーマを作成する方法を学びました。
その後、WordPressにテーマをアップロードし、それをアクティブにしました。

テーマはまだWordPressを経由して追加したすべてのコンテンツを表示していません。
ここからテンプレートファイルにループを追加する必要があります。

現時点では、テーマに一つのメインテンプレートファイル-index.php があります。ここにループを追加します。

##What You’ll Need
-必要なもの-

* エディタ
* ブラウザ 
* スクリーンショットを保存するためのソフト
* インストールされたWordPress （ローカルもしくはリモート）
* ローカルで作業する場合は、WordPressを実行するためのMAMP、WAMPまたはLAMPが必要です
* リモートで作業する場合はFTPのアクセス及び管理者アカウントが必要になります。

##1.Adding a Page in WordPress
-WordPressでのページ追加-  
WordPressを管理者としてページを追加する方法、をすでに知っているものとしてすすめます。
新しいページのコンテンツとして、静的なサイトのコンテンツより、コンテンツ幅サイズの画像部分を除いて利用します。
画像の追加に関しては、本シリーズのパート10で学べますので、今は先行してページを作成します。
そして、必要であれば**「表示設定」**ページで、新しいページをホームページに設定します。

##2. Adding a Loop
-ループを追加する-  
新しくページを作成し、改めてサイトのホームページにアクセスしてみてください。何も変わっていないと思います。
それは、ＷｏｒｄＰｒｅｓｓがページのコンテンツを表示していないのです。
それをさせるため、ループを追加する必要があります。
ループはデータベースからページのコンテンツを引き出す動作をWordPressに与えるものです。

index.phpファイルを開きます。
content divの後ろと&lt;article&gt;タグの前に、以下を追加します。

```
<?php while ( have_posts() ) : the_post(); ?>
```

すぐ後の&lt;/article%gt;タグの後ろに以下を追加します。

```
<?php endwhile; ?>
```
最初のコードの部分はループの始まりです。
そこに表示させる投稿、またはページの有無をチェックし、あればそれらを表示します。

アーカイブページであれば、名ブログページの最新の投稿か、カテゴリページ上の指定されたカテゴリ内の投稿であれば、全ての関連する投稿をループします。

WordPressがサイドバーやフッターなどのコンテンツを表示するように進むため、コードの第2部分でループの終了を行っています。

##3. Classes and IDs for the Article
-ArticleのIDとクラス-  
最初の&lt;article&gt;タグはWordPressによって自動的に生成されたIDやclassを持つことが出来ます。
それにより、その投稿やページをターゲットにCSSを利用することが出来ます。

&lt;article&gt;の開始タグを探します。

```
<article class="post" id="01">
```

編集します

```
<article class="<?php post_class(); ?>" id="post-<?php the_ID(); ?>">
```

追加した2つの機能は以下のとおりです。

* the_ID()…表示されている投稿もしくはページを参照するためのユニークなIDをarticle要素に対して追加します。
* post_class…投稿カテゴリや投稿タイプなどを含む、articleの要素に対して、一連のclassが追加されます。





