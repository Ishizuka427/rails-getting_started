# rails-getting_started

サーバー起動
```sh
$ bin/rails server
```
http://127.0.0.1:3000/

---

To-Do
- [ ] [9 リファクタリング](https://railsguides.jp/getting_started.html#%E3%83%AA%E3%83%95%E3%82%A1%E3%82%AF%E3%82%BF%E3%83%AA%E3%83%B3%E3%82%B0) から進める

[Rails をはじめよう](https://railsguides.jp/getting_started.html) の個人的 memo

```console
$ gem install rails
$ mkdir rails-getting_started
$ cd rails-getting_started
$ rails new blog
      create  
      create  README.md
      create  Rakefile
      create  .ruby-version
      create  config.ru
      create  .gitignore
      create  .gitattributes
      create  Gemfile
         run  git init from "."
...

$ tree -L 2
.
├── Gemfile
├── Gemfile.lock
├── README.md
├── Rakefile
├── app
│   ├── assets
│   ├── channels
│   ├── controllers
│   ├── helpers
│   ├── javascript
│   ├── jobs
│   ├── mailers
│   ├── models
│   └── views
├── bin
│   ├── bundle
│   ├── importmap
│   ├── rails
│   ├── rake
│   └── setup
├── config
│   ├── application.rb
│   ├── boot.rb
│   ├── cable.yml
│   ├── credentials.yml.enc
│   ├── database.yml
│   ├── environment.rb
│   ├── environments
│   ├── importmap.rb
│   ├── initializers
│   ├── locales
│   ├── master.key
│   ├── puma.rb
│   ├── routes.rb
│   └── storage.yml
├── config.ru
├── db
│   └── seeds.rb
├── lib
│   ├── assets
│   └── tasks
├── log
│   └── development.log
├── public
│   ├── 404.html
│   ├── 422.html
│   ├── 500.html
│   ├── apple-touch-icon-precomposed.png
│   ├── apple-touch-icon.png
│   ├── favicon.ico
│   └── robots.txt
├── storage
├── test
│   ├── application_system_test_case.rb
│   ├── channels
│   ├── controllers
│   ├── fixtures
│   ├── helpers
│   ├── integration
│   ├── mailers
│   ├── models
│   ├── system
│   └── test_helper.rb
├── tmp
│   ├── cache
│   ├── development_secret.txt
│   ├── pids
│   └── storage
└── vendor
    └── javascript
```

## [3.2 ブログアプリケーションを作成する](https://railsguides.jp/getting_started.html#%E3%83%96%E3%83%AD%E3%82%B0%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B)

- Rackとは？ [Rack](https://rack.github.io/)
Rubyにおいて、アプリケーションサーバ(Puma、Unicornなど)とWebアプリケーションやフレームワークを接続するための標準化インターフェース(規約)
- Bundlerとは？ [Bundler](https://bundler.io/)
仮想環境構築 ＋ Gemの管理。Python でいう venv みたいなもの
- Rakefileとは？
Ruby 用 Makefile
- Active Storageとは？ [Active Storage](https://railsguides.jp/active_storage_overview.html)
ファイルの Upload と Storage を簡単に管理するためのライブラリ
- gitattributesとは？ [gitattributes](https://git-scm.com/docs/gitattributes)
Git リポジトリ内のファイルの動作や表示を制御するために使用される設定ファイル

## [4.1 Webサーバーを起動する](https://railsguides.jp/getting_started.html#web%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E3%82%92%E8%B5%B7%E5%8B%95%E3%81%99%E3%82%8B)
```console
$ bin/rails server
```
 http://localhost:3000

![image](https://github.com/Ishizuka427/rails-getting_started/assets/56011102/dcded022-c979-4ec5-ade7-2f91965db8f8)

## [4.2 Railsで「Hello」と表示する](https://railsguides.jp/getting_started.html#rails%E3%81%A7%E3%80%8Chello%E3%80%8D%E3%81%A8%E8%A1%A8%E7%A4%BA%E3%81%99%E3%82%8B)
- ルーティングとは？
HTTPリクエストのURLを対応するコントローラのアクションに結び付ける仕組みのこと
config/routes.rbファイルで定義される
- コントローラとは？
Railsアプリケーション内でビジネスロジックを実装するためのクラス
HTTPリクエストを受け取り、適切な処理を行った後にレスポンスを返す
- 例
"/articles"という URL で GETリクエストが来た場合、ルーティングはそれを Articlesコントローラの indexアクションに結び付ける。※ indexアクションは、記事の一覧を表示するための処理を担当する

![image](https://github.com/Ishizuka427/rails-getting_started/assets/56011102/c9297242-cc94-4434-a3a6-66323b94760a)

参照: https://isle3.net/ruby-on-rails-routing-controller-view/

```rb:/config/routes.rb 
Rails.application.routes.draw do
  get "/articles", to: "articles#index"
  # Define your application routes per the DSL in https://guides.rubyonrails.org/routing.html

  # ...
end
```
### コントローラ用のジェネレータを実行

```console
$ bin/rails generate controller Articles index --skip-routes
      create  app/controllers/articles_controller.rb
      invoke  erb
      create    app/views/articles
      create    app/views/articles/index.html.erb
      invoke  test_unit
      create    test/controllers/articles_controller_test.rb
      invoke  helper
      create    app/helpers/articles_helper.rb
      invoke    test_unit
```
#### 生成されたファイル
ファイルの種類 | 場所
-- | --
コントローラファイル | `app/controllers/articles_controller.rb`

```rb:app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  def index
  end
end
```

- `index`アクションが空の場合、コントローラー＆アクションから自動的に合うビューをレンダリングする
- デフォルトで `app/views/articles/index.html.erb` をレンダリング

`app/views/articles/index.html.erb` を以下のように編集して保存
```erb:app/views/articles/index.html.erb
<h1>Hello, Rails!</h1>
```
http://localhost:3000/articles

## [6.1 モデルを生成する](https://railsguides.jp/getting_started.html#%E3%83%A2%E3%83%87%E3%83%AB%E3%82%92%E7%94%9F%E6%88%90%E3%81%99%E3%82%8B)
> モデル（model）とは、データを表現するためのRubyクラスです。モデルは、Active Recordと呼ばれるRailsの機能を介して、アプリケーションのデータベースとやりとりできます。

Active Recordとは？  
図解  

![image](https://github.com/Ishizuka427/rails-getting_started/assets/56011102/88fa8d0a-ab3d-44a1-bcd3-f02137b590f7)

参照: https://qiita.com/ryokky59/items/a1d0b4e86bacbd7ef6e8

### モデル用のジェネレータを実行
モデル名: Article -> 必ず単数形。モデルのクラス名が2語以上の場合は CamelCase  
カラム: title, body
```console
$ bin/rails generate model Article title:string body:text
      invoke  active_record
      create    db/migrate/20230601072728_create_articles.rb
      create    app/models/article.rb
      invoke    test_unit
      create      test/models/article_test.rb
      create      test/fixtures/articles.yml
```
#### 生成されたファイル
ファイルの種類 | 場所
-- | --
マイグレーションファイル | `db/migrate/<タイムスタンプ>_create_articles.rb`
モデルファイル | `app/models/article.rb`

```rb:db/migrate/20230601072728_create_articles.rb 
class CreateArticles < ActiveRecord::Migration[7.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :body

      t.timestamps
    end
  end
end
```
- `create_table`メソッド呼び出しは、`articles`テーブルの構成方法を指定している
- `create_table`のブロック内には、`titleとbody`という2つのカラムが定義されている

マイグレーションを実行
```console
$ bin/rails db:migrate                         
== 20230601072728 CreateArticles: migrating ===================================
-- create_table(:articles)
   -> 0.0031s
== 20230601072728 CreateArticles: migrated (0.0031s) ==========================
```

## [6.3 モデルを用いてデータベースとやりとりする](https://railsguides.jp/getting_started.html#%E3%83%A2%E3%83%87%E3%83%AB%E3%82%92%E7%94%A8%E3%81%84%E3%81%A6%E3%83%87%E3%83%BC%E3%82%BF%E3%83%99%E3%83%BC%E3%82%B9%E3%81%A8%E3%82%84%E3%82%8A%E3%81%A8%E3%82%8A%E3%81%99%E3%82%8B)
- Railsコンソールとは？
Ruby の irb。対話的コーディング環境

```console
$ bin/rails console
Loading development environment (Rails 7.0.5)
```

title と body を更新する

```rb
irb(main):001:0>  article = Article.new(title: "Hello Rails", body: "I am on Rails!")
=> #<Article:0x00000001063b49d8 id: nil, title: "Hello Rails", body: "I am on Rails!", created_at: nil, updated_at: nil>
```
※ まだデータベースに保存されていない

### 記事をデータベースに保存
オブジェクトをデータベースに保存するには、`save`メソッドを呼び出す

```rb
irb(main):002:0>  article.save
  TRANSACTION (0.1ms)  begin transaction
  Article Create (1.6ms)  INSERT INTO "articles" ("title", "body", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["title", "Hello Rails"], ["body", "I am on Rails!"], ["created_at", "2023-06-01 08:16:12.164139"], ["updated_at", "2023-06-01 08:16:12.164139"]]
  TRANSACTION (1.8ms)  commit transaction
=> true
```
`article`オブジェクトを表示
```rb
irb(main):003:0>  article
=> 
#<Article:0x00000001063b49d8
 id: 1,
 title: "Hello Rails",
 body: "I am on Rails!",
 created_at: Thu, 01 Jun 2023 08:16:12.164139000 UTC +00:00,
 updated_at: Thu, 01 Jun 2023 08:16:12.164139000 UTC +00:00>
```
オブジェクトに属性（attribute）が設定されている  
※ オブジェクトを`save`したときにRailsが追加
- id
- created_at
- updated_at

### 記事をデータベースから取り出す
対象のモデルで`find`メソッドを呼び出し、取得したい記事のidを引数として渡す
```rb
irb(main):004:0> Article.find(1)
  Article Load (0.8ms)  SELECT "articles".* FROM "articles" WHERE "articles"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
=> 
#<Article:0x0000000107b1b7c0
 id: 1,
 title: "Hello Rails",
 body: "I am on Rails!",
 created_at: Thu, 01 Jun 2023 08:16:12.164139000 UTC +00:00,
 updated_at: Thu, 01 Jun 2023 08:16:12.164139000 UTC +00:00>
```
データベースに保存されているすべての記事を取り出すには、対象のモデルで`all`メソッドを呼び出す
```rb
irb(main):005:0> Article.all
  Article Load (0.4ms)  SELECT "articles".* FROM "articles"
=> 
[#<Article:0x0000000107b13c00
  id: 1,
  title: "Hello Rails",
  body: "I am on Rails!",
  created_at: Thu, 01 Jun 2023 08:16:12.164139000 UTC +00:00,
  updated_at: Thu, 01 Jun 2023 08:16:12.164139000 UTC +00:00>]
```
## [6.4 記事のリストを表示する](https://railsguides.jp/getting_started.html#%E8%A8%98%E4%BA%8B%E3%81%AE%E3%83%AA%E3%82%B9%E3%83%88%E3%82%92%E8%A1%A8%E7%A4%BA%E3%81%99%E3%82%8B)
コントローラファイルを開いて`index`アクションを変更  
-> データベースからすべての記事を取り出せるようにする
```rb:app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
end
```

ビューファイル`app/views/articles/index.html.erb`内にインスタンス変数（@で始まる変数）`@articles` と書くと、参照することができる

```erb:app/views/articles/index.html.erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= article.title %>
    </li>
  <% end %>
</ul>
```

### ERB（Embedded Ruby）
Rubyを使用してHTMLやXMLなどのテンプレートを作成するためのテンプレートエンジン  
ERBを使用すると、Rubyのコードをテンプレート内に埋め込むことができ、動的なコンテンツを生成することができる

タグ | 意味
-- | --
`<% %>` | この中のRubyコードを評価する
`<%= %>` | この中のRubyコードを評価し、返された値を出力する

Rails server を起動してみてみる
http://localhost:3000/

<img width="329" alt="スクリーンショット 2023-06-02 14 01 45" src="https://github.com/Ishizuka427/rails-getting_started/assets/56011102/d988edce-c895-4a63-ac8e-34444d2237bc">

## [7.1 記事を1件表示する](https://railsguides.jp/getting_started.html#%E8%A8%98%E4%BA%8B%E3%82%921%E4%BB%B6%E8%A1%A8%E7%A4%BA%E3%81%99%E3%82%8B)

```rb:config/routes.rb
Rails.application.routes.draw do
  root "articles#index"

  get "/articles", to: "articles#index"
  get "/articles/:id", to: "articles#show"
end
```
### `:id` とは？
ルーティングのパラメータ（parameter）
たとえば`GET http://localhost:3000/articles/1`というリクエストを扱う場合`:id`で1がキャプチャされて`params` ハッシュに保存される。
※ `params` はコントローラのアクションでもアクセスできる

`show`アクションを`app/controllers/articles_controller.rb`の`index`アクションの下に追加

```rb:app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end
end
```
`show`アクションでやっていること
- `Article.find`メソッドを呼び出し
- `params` から`:id` を受け取る
- 返された記事は`@article`インスタンス変数に保存
　
※ `show`アクションは、デフォルトで`app/views/articles/show.html.erb`をレンダリング

```erb:app/views/articles/show.html.erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>
```
http://localhost:3000/articles/1

記事に飛ぶリンクの追加
```erb:app/views/articles/index.html.erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <a href="/articles/<%= article.id %>">
        <%= article.title %>
      </a>
    </li>
  <% end %>
</ul>
```

<img width="380" alt="スクリーンショット 2023-06-02 17 23 42" src="https://github.com/Ishizuka427/rails-getting_started/assets/56011102/f5b87159-7f11-433a-9b1f-5bc1acbafc8c">


## [7.2 リソースフルルーティング](https://railsguides.jp/getting_started.html#%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E3%83%95%E3%83%AB%E3%83%AB%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0)

### CRUD（Create、Read、Update、Delete）を追加するときは以下の3つの作業を行う
1. ルーティングを追加する
2. コントローラにアクションを追加する
3. ビューを追加する

`config/routes.rb`でこれまで`get`メソッドで書かれていたルーティングを`resources`で書き換える

```rb:config/routes.rb
Rails.application.routes.draw do
  root "articles#index"

  resources :articles
end
```

### `bin/rails routes`コマンド
ルーティングがどのように対応付けられているかを表示する
```console
$ bin/rails routes
      Prefix Verb   URI Pattern                    Controller#Action
         root GET   /                              articles#index
     articles GET   /articles(.:format)            articles#index
             POST   /articles(.:format)            articles#create
  new_article GET   /articles/new(.:format)        articles#new
 edit_article GET   /articles/:id/edit(.:format)   articles#edit
      article GET   /articles/:id(.:format)        articles#show
            PATCH   /articles/:id(.:format)        articles#update
              PUT   /articles/:id(.:format)        articles#update
           DELETE   /articles/:id(.:format)        articles#destroy
(略)
```
- `_url` URLヘルパーメソッド
- `_path` パスヘルパーメソッド

```erb:app/views/articles/index.html.erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <a href="<%= article_path(article) %>">
        <%= article.title %>
      </a>
    </li>
  <% end %>
</ul>
```

`link_to`ヘルパー
- 第1引数: リンクテキスト
- 第2引数: リンク先  
第2引数にモデルオブジェクトを渡すと、`link_to`が適切なパスヘルパーを呼び出してオブジェクトをパスに変換する

```erb:app/views/articles/index.html.erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= link_to article.title, article %>
    </li>
  <% end %>
</ul>
```

## [7.3 記事を1件作成する](https://railsguides.jp/getting_started.html#%E8%A8%98%E4%BA%8B%E3%82%921%E4%BB%B6%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B)

```rb:app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(title: "...", body: "...")

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end
end
```

### newアクションとcreateアクションの違い
#### newアクション
新しいオブジェクトを作成するための準備を行う
- 具体的には: 
データベースに保存するための新しいオブジェクトをメモリ上に作成し、それに関連するフォームを表示する
- 例: 
ブログ記事の作成ページを開く際に、newアクションが呼び出される  
このアクションでは、データベースに保存する前の新しいブログ記事のインスタンスを作成し、それを表現するためのフォームを表示することが一般的。
#### createアクション
newアクションで作成されたオブジェクトを実際にデータベースに保存する
※ createアクションは通常、newアクションの後に呼び出される
- 具体的には: 
フォームから受け取ったデータを使って新しいオブジェクトを作成し、それをデータベースに保存する
- 例: 
ブログ記事の作成ページでフォームに入力した内容を受け取り、それを使って実際のブログ記事を作成し、データベースに保存するためにcreateアクションが呼び出される。

## [7.3.1 フォームビルダーを使う](https://railsguides.jp/getting_started.html#%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%83%93%E3%83%AB%E3%83%80%E3%83%BC%E3%82%92%E4%BD%BF%E3%81%86)

Railsのフォームビルダー（form builder）は、RailsアプリケーションでHTMLフォームを作成する際に便利なツール。フォームビルダーを使用すると、簡単にフォームフィールドやラベル、エラーメッセージなどを生成することができる。

```erb:app/views/articles/new.html.erb
<h1>New Article</h1>

<%= form_with model: @article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
`form_with`メソッドを使用してフォームを作成している。`model`オプションを指定することで、フォームが関連付けられるモデルオブジェクトを指定できる。フォーム内の各フィールドは、`form.label`と`form.field_type`メソッドを使用して定義される。  
  
※ `form_with`を呼び出したときの出力結果は以下
```erb
<form action="/articles" accept-charset="UTF-8" method="post">
  <input type="hidden" name="authenticity_token" value="...">

  <div>
    <label for="article_title">Title</label><br>
    <input type="text" name="article[title]" id="article_title">
  </div>

  <div>
    <label for="article_body">Body</label><br>
    <textarea name="article[body]" id="article_body"></textarea>
  </div>

  <div>
    <input type="submit" name="commit" value="Create Article" data-disable-with="Create Article">
  </div>
</form>
```

## [7.3.2 Strong Parametersを使う](https://railsguides.jp/getting_started.html#strong-parameters%E3%82%92%E4%BD%BF%E3%81%86)
Strong Parametersは、Ruby on Railsフレームワークにおいて、セキュリティとマスアサインメントの問題に対処するために使用される。マスアサインメントとは、複数の属性をまとめて一括で更新することを指す。  
  
ここで言う`strong`とは、`params`を強く型付けする（strong typing）という意味

- 末尾に article_paramsというprivateメソッドを追加し、paramsをフィルタする
- createアクションでこのメソッドを使うように変更する

```rb:app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end

  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```

### [7.3.3 バリデーションとエラーメッセージの表示](https://railsguides.jp/getting_started.html#%E3%83%90%E3%83%AA%E3%83%87%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%A8%E3%82%A8%E3%83%A9%E3%83%BC%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8%E3%81%AE%E8%A1%A8%E7%A4%BA)

```rb:app/models/article.rb
class Article < ApplicationRecord
  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```

> `validates :title, presence: true`

- titleの値が必ず存在しなければならない
- titleは文字列なので、titleにはホワイトスペース（スペース文字、改行、Tabなど）以外の文字が1個以上含まれていなければならない

>  validates :body, presence: true, length: { minimum: 10 }

- bodyの値が必ず存在しなければならない
- bodyの値は10文字以上でなければならない


```erb:app/views/articles/new.html.erb
<h1>New Article</h1>

<%= form_with model: @article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
    <% @article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %><br>
    <% @article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

http://localhost:3000/articles/new

<img width="381" alt="スクリーンショット 2023-06-06 15 00 40" src="https://github.com/Ishizuka427/rails-getting_started/assets/56011102/eeadbeb6-db50-40f0-bc67-3b9772324cad">


## [7.3.4 仕上げ](https://railsguides.jp/getting_started.html#%E8%A8%98%E4%BA%8B%E3%82%921%E4%BB%B6%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B-%E4%BB%95%E4%B8%8A%E3%81%92)

[New Article](http://localhost:3000/articles/new) の追加

```erb:app/views/articles/index.html.erb

<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= link_to article.title, article %>
    </li>
  <% end %>
</ul>

<%= link_to "New Article", new_article_path %>
```
http://localhost:3000/articles/

<img width="393" alt="スクリーンショット 2023-06-06 15 13 01" src="https://github.com/Ishizuka427/rails-getting_started/assets/56011102/1ee44341-04e1-418b-b54a-0440eb1338d9">

## [7.4 記事を更新する](https://railsguides.jp/getting_started.html#%E8%A8%98%E4%BA%8B%E3%82%92%E6%9B%B4%E6%96%B0%E3%81%99%E3%82%8B)

更新のステップは、コントローラの`edit`アクションと`update`アクションで扱う

### `edit`アクション
編集フォームを表示するためのアクション  
具体的に: レコードの特定のIDを取得し、それを使用してデータベースから対応するレコードを取得する。そして、そのレコードを編集するためのビューファイル（edit.html.erbなど）を表示する。

### `update`アクション
編集フォームから送信されたデータを処理し、レコードを更新するためのアクション  
具体的に: editアクションと同様に、特定のIDに基づいて対応するレコードを取得する。そして、送信されたデータを使用してそのレコードを更新し、必要な場合にはバリデーションを行う。

```rb:app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
    @article = Article.find(params[:id])
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render :edit, status: :unprocessable_entity
    end
  end

  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```

## [7.4.1 ビューのコードをパーシャルで共有する](https://railsguides.jp/getting_started.html#%E3%83%93%E3%83%A5%E3%83%BC%E3%81%AE%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92%E3%83%91%E3%83%BC%E3%82%B7%E3%83%A3%E3%83%AB%E3%81%A7%E5%85%B1%E6%9C%89%E3%81%99%E3%82%8B)

パーシャル(部分テンプレート)は、Ruby on Rails フレームワークにおける一部のビューテンプレートを再利用するための仕組み

```erb:app/views/articles/_form.html.erb
<%= form_with model: article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
    <% article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %><br>
    <% article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

render でパーシャルを使う
```erb:app/views/articles/new.html.erb
<h1>New Article</h1>

<%= render "form", article: @article %>
```

> パーシャルのファイル名は冒頭にアンダースコア_を必ず付ける（例: `_form.html.erb`）
> ただし、レンダリングでパーシャルを参照するときはアンダースコアを付けない（例: `render "form"`）

```erb:app/views/articles/edit.html.erb
<h1>Edit Article</h1>

<%= render "form", article: @article %>
```

## [7.4.2 仕上げ](https://railsguides.jp/getting_started.html#%E8%A8%98%E4%BA%8B%E3%82%92%E6%9B%B4%E6%96%B0%E3%81%99%E3%82%8B-%E4%BB%95%E4%B8%8A%E3%81%92)

```erb:app/views/articles/show.html.erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
</ul>
```

## [7.5 記事を削除する](https://railsguides.jp/getting_started.html#%E8%A8%98%E4%BA%8B%E3%82%92%E5%89%8A%E9%99%A4%E3%81%99%E3%82%8B)

`destroy`アクションを追加

```rb:app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
    @article = Article.find(params[:id])
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render :edit, status: :unprocessable_entity
    end
  end

  def destroy
    @article = Article.find(params[:id])
    @article.destroy

    redirect_to root_path, status: :see_other
  end

  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```

削除用ボタンを追加

```erb:app/views/articles/show.html.erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>
```

## [8 モデルを追加する](https://railsguides.jp/getting_started.html#%E3%83%A2%E3%83%87%E3%83%AB%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B)

```console
$ bin/rails generate model Comment commenter:string body:text article:references
      invoke  active_record
      create    db/migrate/20230606065420_create_comments.rb
      create    app/models/comment.rb
      invoke    test_unit
      create      test/models/comment_test.rb
      create      test/fixtures/comments.yml
```

ファイル | 目的
-- | --
db/migrate/20140120201010_create_comments.rb | データベースにコメント用のテーブルを作成するためのマイグレーションファイル（ファイル名のタイムスタンプはこれとは異なります）
app/models/comment.rb | Commentモデル
test/models/comment_test.rb | Commentモデルをテストするためのハーネス
test/fixtures/comments.yml | テストで使うサンプルコメント

```ruby:app/models/comment.rb
class Comment < ApplicationRecord
  belongs_to :article
end
```
- `belongs_to :article`: Active Recordの関連付け
- `:references`型: 指定されたモデル名の後ろに`_id`を追加した名前を持つ新しいカラムをデータベーステーブルに作成する

```ruby:db/schema.rb
class CreateComments < ActiveRecord::Migration[7.0]
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      t.references :article, null: false, foreign_key: true

      t.timestamps
    end
  end
end
```

`t.references` の行で設定していること: 
- `article_id`という名前のint型カラムとそのインデックス
- `articles`の`id`カラムを指す外部キー制約を設定

```console
$ bin/rails db:migrate
== 20230606065420 CreateComments: migrating ===================================
-- create_table(:comments)
   -> 0.0062s
== 20230606065420 CreateComments: migrated (0.0063s) ==========================
```

## [8.2 モデル同士を関連付ける](https://railsguides.jp/getting_started.html#%E3%83%A2%E3%83%87%E3%83%AB%E5%90%8C%E5%A3%AB%E3%82%92%E9%96%A2%E9%80%A3%E4%BB%98%E3%81%91%E3%82%8B)

- 1件のコメントは1件の記事に属する（Each comment **belongs to** one article）
- 1件の記事はコメントを複数持てる（One article can **have many** comments）

Commentモデル（app/models/comment.rb）  
コードに既に書かれていたように、各コメントは1つの記事に属している

```ruby
class Comment < ApplicationRecord
  belongs_to :article
end
```

Articleモデル（app/models/article.rb）  
関連付けの他方のモデルをここに追加する必要がある

```ruby
class Article < ApplicationRecord
  has_many :comments

  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```

これらによって  
`@article`というインスタンス変数に記事が1件含まれていれば、`@article.comments`と書くだけでその記事に関連付けられているコメントをすべて取得できる

## [8.3 コメントへのルーティングを追加する](https://railsguides.jp/getting_started.html#%E3%82%B3%E3%83%A1%E3%83%B3%E3%83%88%E3%81%B8%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B)

`articles`の内側にネストしたリソース（nested resouce）として`comments`を作成する  
※ モデルの記述とは別の視点から、記事とコメントの間のリレーションシップを階層的に捉えたもの

```ruby:config/routes.rb
ails.application.routes.draw do
  root "articles#index"

  resources :articles do
    resources :comments
  end
end
```

## [8.4 コントローラを生成する](https://railsguides.jp/getting_started.html#%E3%82%B3%E3%83%B3%E3%83%88%E3%83%AD%E3%83%BC%E3%83%A9%E3%82%92%E7%94%9F%E6%88%90%E3%81%99%E3%82%8B)

```console
$ bin/rails generate controller Comments
      create  app/controllers/comments_controller.rb
      invoke  erb
      create    app/views/comments
      invoke  test_unit
      create    test/controllers/comments_controller_test.rb
      invoke  helper
      create    app/helpers/comments_helper.rb
      invoke    test_unit
```

ファイル/ディレクトリ | 目的
-- | --
app/controllers/comments_controller.rb | コメント用コントローラ
app/views/comments/ | このコントローラのビューはここに置かれる
test/controllers/comments_controller_test.rb | このコントローラのテスト用ファイル
app/helpers/comments_helper.rb | ビューヘルパー

```erb:app/views/articles/show.html.erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>

<h2>Add a comment:</h2>
<%= form_with model: [ @article, @article.comments.build ] do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
```
`Article`モデルの`find`メソッドを最初に呼び出し、リクエストで言及されている記事（のオブジェクト）を取得して@articleに保存する
```ruby:app/controllers/comments_controller.rb
class CommentsController < ApplicationController
  def create
    @article = Article.find(params[:article_id])
    @comment = @article.comments.create(comment_params)
    redirect_to article_path(@article)
  end

  private
    def comment_params
      params.require(:comment).permit(:commenter, :body)
    end
end
```
`@article.comments`に対して`create`メソッドを実行することで、コメントの作成と保存を同時に行っている
-> コメントと記事が自動的にリンクされる

```erb:app/views/articles/show.html.erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>

<h2>Comments</h2>
<% @article.comments.each do |comment| %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>

  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>

<h2>Add a comment:</h2>
<%= form_with model: [ @article, @article.comments.build ] do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

<img width="521" alt="スクリーンショット 2023-06-06 17 12 23" src="https://github.com/Ishizuka427/rails-getting_started/assets/56011102/fb94b8c4-095d-4a08-9919-a9bcb0657ab6">


## [9 リファクタリング](https://railsguides.jp/getting_started.html#%E3%83%AA%E3%83%95%E3%82%A1%E3%82%AF%E3%82%BF%E3%83%AA%E3%83%B3%E3%82%B0)
done

次: 
9.3 concernを使う
