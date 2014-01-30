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

例えば、CSSで特定の投稿をターゲットにするIDを使用することができ、classは特定のカテゴリと同じ方法で、全ての投稿にスタイルを適用させることが出来ます。

##4. Adding the Page or Post Title in the Loop
-ループ内のページや記事のタイトル追加- 

投稿やページに表示される次のものがタイトルで、既存のコードでは&lt;h2&gt;タグで固定されたタイトルです。
読んでその行を探します。

```
<h2 class="entry-title">This is the title of a post or page</h2>
```

編集します。

```<h2 class="entry-title"><a title="<?php printf( esc_attr__( 'Permalink to %s', 'compass' ), the_title_attribute( 'echo=0' ) ); ?>" href="<?php the_permalink(); ?>" rel="bookmark">
    <?php the_title(); ?>
</a></h2>
```

これは2つのことを追加しています。

* 投稿やページ自体（ the_permalink() の使用）へのリンク。これにより、ユーザーは投稿自体のページへのリンクをクリック出来るようになるため、アーカイブページを使うのに便利になります。
* 投稿やページのタイトルが、WordPressによって自動的に移入されます。

##5. Adding Post Metadata
-ポストメタデータの追加- 

ループ内最初のsection要素はポストメタデータ - 投稿日、日付、著者です。
コードを見つけましょう。（最初のsection要素もしくは、全てのコード：テーマ内で異なっていても構いません。）

```
Posted on 5 November by Rachel McCollin
```

を下記に変えて下さい。

```
Posted on <?php the_date(); ?> by <?php the_author(); ?>
```

次の2つのテンプレートタグを追加しました。

* 投稿が公開された日付：the_date()
* 投稿の著者：the_author()

##Adding the Post Content
-投稿コンテンツの追加- 

最も重要な事は、投稿もしくはページの内容が表示されることです。それを行うにはthe_content()というシンプルな一つのテンプレートタグを利用します。

sectionからクラス（.entry-content）を探し、その内容を削除し、the_content（）タグに置き換えて下記のようにします。

```
<section class="entry-content"><?php the_content(); ?></section><!-- .entry-content -->
```

##More Post Metadata
-ポストメタデータをさらに-  

このデザインでは、より多くのポストメタデータが、投稿やページのコンテンツの後ろに存在します。
これはオプションですが、ここでは投稿に関連付けられているカテゴリのリストを表示するためにそれを利用しています。
ただし、デザインやカテゴリやタグの使用に応じて、ご自身のテーマからは外すことを選択するかもしれません。

最後のsectionの内容を削除し、class(.entry-meta)としてsection全体を読み取り、それらを以下のように交換して下さい。

```
<section class="entry-meta"><?php if ( count( get_the_category() ) ) : ?>
    <span class="cat-links">
        Categories: <?php echo get_the_category_list( ', ' ); ?>
    </span>
<?php endif; ?></section><!-- .entry-meta -->
```

これまで追加したそれは、PHPの長いスニペットのように、このコードを介して動作するよう、時間を取る価値があります。
* 最初の行はif文を利用し、投稿に割り当てられたカテゴリの数をチェックして、0位上であれば残りのコードが実行されるようにしています。
* その後、span要素を開き、echo get_the_catgeory_list()を利用して、その中に投稿のカテゴリを示します。echoはget_the_category_list()の機能と同様に重要で、 get_the_category_list()関数では実際にリストは表示されません。それはリストにアクセスしても何もしません。
* WordPressが次のコードに進めるように、endifにてif文を閉じます。

最後にindex.phpファイルを保存し、ブラウザに戻って画面をリフレッシュします。
以下の様にわずかにですが、変更されているはずです。

ご覧のように、次の項目が表示されます。
* ページのタイトル
* 日付と著者
* ページのコンテンツ
* カテゴリのリストは、このページとは違った投稿のように表示されます。カテゴリは、デフォルトではページには適用されません。シリーズの後半で表示されたカテゴリリストの例を見ることが出来ます。

ノート：画像がまだ表示されていないことに注意して下さい。この連載の項目10にてそれを修正します。




