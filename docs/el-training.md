# el-training

## Original Contents (Japanese)

https://github.com/everyleaf/el-training

## About this curriculum

This document is a curriculum for training new employees to learn the basics of Ruby on Rails and its peripheral technologies.

Slightly customized for Neumann.

## Overview

## System Requirements

In this curriculum, you will develop a task management system as your assignment.
In the task management system, we would like to do the following

- We want to be able to register my tasks easily.
- We want to be able to set an end date for my tasks.
- We want to be able to prioritize my tasks.
- We want to be able to manage the status of tasks (Started, Not Started, Completed).
- We want to narrow down tasks by status.
- We want to search tasks by task name or task description.
- We want to see a list of tasks. We want to sort tasks in the list screen (based on priority, due date, etc.)
- We want to classify tasks with labels.
- We want to register as a user and be able to see only the tasks I have registered.

In addition, we would like to have the following management functions to meet the above requirements.

- User management functions

### Supported Browsers

- The latest version of macOS/Chrome is assumed to be supported.

### Application (server) configuration

We would like you to build it using the following languages and middleware (all of them are the latest stable versions).

- Ruby
- Ruby on Rails
- PostgreSQL

For the server, we would like you to use the following

- Heroku

- We don't have any specific performance or security requirements, but please make sure your site is of general quality. If the response time of the site is too bad, we will ask you to improve it.

## End goal of this curriculum

At the end of this curriculum, students are expected to be able to master the following items.

- Be able to implement a basic web application using Rails.
- Be able to publish a Rails application using common environments.
- Be able to add features and maintain data to published Rails applications.
- To be able to learn the process of PR and merging on GitHub. Also, learn the Git commands necessary for this.
  - To be able to commit with appropriate granularity.
  - To be able to write an appropriate PR description.
  - Be able to respond to reviews and make corrections.
- To be able to ask questions to team members or other relevant people via chat or other means at the right time if something is unclear.

## Recommended Books

We recommend the following books as recommended reading for the training curriculum.

- [Agile Web Development with Rails 6](https://pragprog.com/titles/rails6/agile-web-development-with-rails-6/)

Or original contents Japanese Book.

- [現場で使える Ruby on Rails 5速習実践ガイド](https://book.mynavi.jp/ec/products/detail/id=93905)

## Useful topics for development

Topics that could not be included in a specific assignment step but should be used are listed in topics.md. Please refer to it and use it as needed in implementing the curriculum.

## Assignment Steps

### Step 1: Let's set up a Rails development environment.

#### 1-1: Install Ruby

- Use [rbenv](https://github.com/rbenv/rbenv) to install the latest version of Ruby
- Make sure the `ruby -v` command shows the version of Ruby

#### 1-2: Install Rails

- Let's install Rails with the Gem command
- Make sure you have the latest version of Rails installed
- Make sure you can see the version of Rails with the `rails -v` command

#### 1-3: Install the database (PostgreSQL)

- Let's install PostgreSQL on your OS.

### Step 2: Create a repository on GitHub.

- Install Git on your computer.
- Come up with a name for your app (= repository name)
- Create your repository.
  - If you don't have an account, get one.
  - Then, create an empty repository

### Step 3: Let's create a Rails project.

- Use the `rails new` command to create the minimum required directories and files for your application.
  - If you use the -d postgresql option when running rails new, step 5 will be easier
- Create a directory called `docs` directly under the `rails new` project directory (the directory of your app name) and commit this documentation file.
  - This is to keep the specification of the app under control and available for viewing at any time.
- Push your app to the repository you created on GitHub.
- Put the version of Ruby you're using in your `Gemfile` (make sure Rails already has a version listed).

### Step 4: Think about the application you want to build.

- Before proceeding with the design, think about what kind of application you want to create. (Screen design by paper prototyping is recommended.
  - Also, think about how the application will be used (will it be published on the Internet, for internal use, etc...).
- Read the requirements of the system and think about the data structure you need.
  - What kind of model (tables) do you need?
  - What kind of information is needed in the tables?
- Once you have a data structure in mind, draw it by hand in an ER diagram or model diagram.
  - When you are done, take a picture of it and put it in the repository.
  - Describe the table schema in `README.md` (model name, column name, data type)

There is no need to create a model diagram for the correct answer at this time. It is not necessary to create the correct model diagram at this time, but let's make it as an assumption at this time (if you think it is wrong in future steps, you can modify it).

### Step 5: Configure the database connection (perimeter settings).

- First, create a new topic branch in Git.
  - After that, you can work on the topic branch and commit.
- Install `pg` (database driver for PostgreSQL) in `Gemfile`.
- Configure the `database.yml`.
- Create a database with the command `rails db:create`.
- Check the connection to the database with the `rails db` command.
- Create a PR on GitHub and have it reviewed.
  - When you are working on a project and want others to review it, submit a PR in Draft or WIP (Work In Progress).
  - If you get comments, please respond to them.
  - In our work, we merge into the master branch when it is Approved (= LGTM, Looks Good To Me), but there are days when the reviewer is not available, so you can merge into master without review.
    - If there are comments that need to be fixed later, please do so at that time.

### Step 6: Configure RuboCop
- Let's set up RuboCop as a linter/formatter.
- For this curriculum, we'll use [retrieva-cop](https://github.com/retrieva/retrieva-cop), which has been tweaked to work with Rails apps.
- Install [retrieva-cop](https://github.com/retrieva/retrieva-cop) in your `Gemfile`.
- Install GitHub Actions so that RuboCop will run when you create a PR.
  - Considering the level of difficulty, it is also acceptable for a supporter to run it.
- After that, let's discuss and update the coding conventions as needed.

### Step 7: Let's create a task model.

Let's create a CRUD to manage the tasks.
First, let's create a simple structure where only the name and details can be registered.

- Use the `rails generate` command to create the model classes needed for the task CRUD.
- Let's create a migration and use it to create a table.
  - It is important to ensure that the migration can be reverted to a previous state! Make it a habit to run `redo` to check!
  - Don't forget to set the DB constraints!
- Make sure that you can connect to the database via a model with the `rails c` command.
  - At this time, let's try to create a record in ActiveRecord.
- Set up validations
  - Let's figure out which column and which validation to add.
- Create a PR on GitHub and have it reviewed

### Step 8: Let's make it possible to view, register, update, and delete tasks.

Let's create a task list screen, detail screen, create screen, edit screen, and delete function.

If you create all these functions at once, your PR will tend to be huge.
Therefore, in Step 8, we will divide the PR into multiple parts.

In future steps, if your PR is likely to be large, consider whether you can split it into two or more PRs.
In other words, it is perfectly fine if the Step and PR are not one-to-one.

### Step 8-1: Create Task List and Detail Screens

- Let's make it possible to display the tasks created in step 7 in the list and detail screens.
- Let's create controllers and views with the `rails generate` command.
  - Consult with your supporters to decide which template engine to use.
- Add the necessary implementations to your controllers and views.
- Edit `routes.rb` so that `http://localhost:3000/` will display the task list screen.
- Explain to your supporter what is going on between the web browser and the server.
- Create a PR on GitHub for them to review.

### Step 8-2: Create and Edit Task Screens

- Let's make it possible to create and edit tasks on the screen.
- Display a flash message on the screen after each creation or update.
  - When a validation error occurs, display the error message on the screen.
- Create a PR on GitHub and have it reviewed

### Step 8-3: Make sure you can delete tasks

- Let's make it possible to delete the task you created.
- Display a flash message on the screen after deletion.
- Create a PR on GitHub and have it reviewed.

### Step 8-4: Look back at the code you've added

- Explain to your supporters about the code you added in steps 8-1 to 8-3.
  - About classes, methods and variables
  - About the process flow

### Step 9: Let's get to know SQL.

- Let's work with the database.
  - Connect to a database with the `rails db` command.
  - Use SQL to browse, create, update, and delete tasks.
- Access the task list screen and check the SQL log.
  - Explain to your supporter what kind of SQL is being executed.
- Check what kind of SQL is executed by the ActiveRecord methods.
  - Try to execute `find`, `where`, etc. with `rails c`.

### ステップ10: テストを書こう

- specを書くための準備をしましょう
  - `spec/spec_helper.rb` 、 `spec/rails_helper.rb` を用意しましょう
- model specをバリデーションに対して書いてみましょう
  - 実際はそれほどバリデーションのテストは書きませんが、model spec への理解を深めるためにやってみましょう
- system specをタスク機能に対して書いてみましょう
- Circle CI に RSpec を連携し、Slackに通知するようにしましょう
  - ステップ6と同様、サポーターが実施する形でも構いません
- 参考書籍：https://leanpub.com/everydayrailsrspec-jp

### ステップ11: アプリの日本語部分を共通化しよう

- Railsのi18nの仕組みを利用して、validation エラーメッセージを日本語で出力するようにしましょう

### ステップ12: Railsのタイムゾーンを設定しよう

- Railsのタイムゾーンを日本（東京）に設定しましょう

### ステップ13: タスク一覧を作成日時の順番で並び替えよう

- 現在IDの順で並んでいますが、これを作成日時の降順で並び替えてみましょう
- 並び替えがうまく行っていることをsystem specで書いてみましょう

### ステップ14: デプロイをしよう

- masterブランチにシンプルなタスク管理システムができたので、デプロイしてみましょう。
- Herokuにデプロイを実施してみましょう
  - アカウントがなければ作成しましょう
- デプロイされたHeroku上のアプリを触ってみましょう
  - これからはこのアプリにタスクを登録して開発を進めましょう
  - ※ ただし、Herokuのアプリケーションはインターネットでどこでも参照できるので、公開してはまずい情報は載せないようにしましょう
    - Basic認証をこの時点でいれてもいいかもしれません
  - 今後、ステップが終わるたびにHerokuへ自分のアプリを継続的にデプロイしましょう
- デプロイの方法を `README.md` に記載しましょう
  - その際に、このアプリで使っているフレームワークのバージョン情報なども記載しておくとなおよいです

### ステップ15: 終了期限を追加しよう

- タスクに対して、終了期限を登録できるようにしてみましょう
- 一覧画面で、終了期限でソートできるようにしましょう
- specを拡充しましょう
- PRしてレビューをしてもらったら、リリースしてみましょう

### ステップ16: ステータスを追加して、検索できるようにしよう

- ステータス（未着手・着手中・完了）を追加してみましょう
  - 【オプション】初学者ではない場合はstateを管理するGemを導入しても構いません
- 一覧画面でタイトルとステータスで検索ができるようにしましょう
  - 【オプション】初学者ではない場合はransackなどの検索の実装を便利にするGemを導入しても構いません
- 絞り込んだ際、ログを見て発行されるSQLの変化を確認してみましょう
  - 以降のステップでも必要に応じて確認する癖をつけましょう
- 検索インデックスを貼りましょう
  - ある程度まとまったテストデータを用意して log/development.log を見ながら動作確認を行い、インデックスの追加により速度が改善されることを確認しましょう
  - 【オプション】PostgreSQLの explain などを使用して、データベース側でのインデックス使用状況なども見てみましょう
- 検索に対してmodel specを追加してみましょう（system specも拡充しておきましょう）

### ステップ17: 優先順位を設定しよう（※類似した実装経験のある人は省略可）

- タスクに対して、優先順位（高中低）を登録できるようにしましょう
- 優先順位でソートできるようにしましょう
- system specを拡充しましょう
- PRしてレビューをしてもらったら、リリースしてみましょう（以降続けてください）

### ステップ18: ページネーションを追加しよう

- KaminariというGemを使って一覧画面にページネーションを追加してみましょう

### ステップ19: デザインを当てよう

- Bootstrapを導入して、これまで作成したアプリにデザインを当てましょう
  - 【オプション】自分でCSSを書いてデザインする

### ステップ20: ユーザモデルを作成しよう

- ユーザモデルを作成してみましょう
- 最初のユーザをseedで作成してみましょう
- seedで作った最初のユーザとタスクが紐づくようにしましょう
  - 関連に対してインデックスを貼りましょう
  - ※ Herokuにデプロイした際に、すでに登録されているタスクとユーザが紐づいているようにしてください（データメンテナンス）

### ステップ21: ログイン/ログアウト機能を実装しよう

- 追加のGemを使わず、自分で実装してみましょう
  - DeviseなどのGemを使わないことで、HTTPのCookieやRailsにおけるSessionなどの仕組みについて理解を深めることが目的です
  - また、一般的な認証についての理解を深めることも目的にしています（パスワードの取り扱いについてなど）
- ログイン画面を実装しましょう
- ログインしていない場合は、タスク管理のページに遷移できないようにしましょう
- タスクを作成したときに、タスクをログイン中のユーザに紐付けるようにしましょう
- 自分が作成したタスクだけを表示するようにしましょう
- ログアウト機能を実装しましょう

### ステップ22: ユーザの管理画面を実装しよう

- 画面上に管理メニューを追加しましょう
- 管理画面にはかならず `/admin` というURLを先頭につけるようにしましょう
  - `routes.rb` に追加する前に、あらかじめURLやルーティング名（ `*_path` となる名前）を想定して設計してみましょう
- ユーザ一覧・作成・更新・削除を実装しましょう
- ユーザを削除したら、そのユーザが抱えているタスクを削除するようにしてみましょう
- ユーザの一覧画面で、ユーザが持っているタスクの数を表示するようにしてみましょう
  - N+1問題を回避するための仕組みを取り入れましょう
- ユーザが作成したタスクの一覧が見られるようにしてみましょう

### ステップ23: ユーザにロールを追加しよう

- ユーザに管理ユーザと一般ユーザを区別するようにしてみましょう
- 管理ユーザだけがユーザ管理画面にアクセスできるようにしてみましょう
  - 一般ユーザが管理画面にアクセスした場合、専用の例外を出してみましょう
  - 例外を補足して、適切にエラーページを表示しましょう（ステップ25で実施しても構いません）
- ユーザ管理画面でロールを選択できるようにしましょう
- 管理ユーザが1人もいなくならないように削除の制御をしましょう
  - モデルのコールバックを利用してみましょう
- ※ Gemの使用・不使用は自由です

### ステップ24: タスクにラベルをつけられるようにしよう

- タスクに複数のラベルをつけられるようにしてみましょう
- つけたラベルで検索できるようにしてみましょう

### ステップ25: エラーページを適切に設定しよう

- Railsが用意しているデフォルトのエラーページを自分が作った画面にしてみましょう
- 状況に応じて、適切にエラーページを設定しましょう
  - ステータスコードの404ページと500ページの2種類の設定は少なくとも必須とします

## あとがき

お疲れさまでした。
あなたは教育カリキュラムを一通り完遂しました!!

このカリキュラムでは触れきれませんでしたが、今後は以下のトピックなどが必要になると思うので、学習を進めていくとよいと思います（案件を通じて学ぶことも多いと思います）。

- Webアプリケーションの基本的な理解を深める
  - HTTPとHTTPSに関する理解
- Railsのもう少し進んだ使い方を習得する
  - STI
  - ロギング
  - 明示的なトランザクション
  - 非同期処理
  - アセットパイプライン（どちらかというとリリース系のトピック）
- JavaScriptやCSSなどのフロントエンドに関するより高度な理解
- データベースに対する理解を深める
  - SQL
  - よりパフォーマンスを重視したクエリの構築
  - インデックスの理解をより深める
- サーバ環境に関するより多くの理解
  - Linux OS
  - Webサーバ（Nginx）の設定
  - アプリケーションサーバ（Unicorn）の設定
  - PostgreSQLに関する設定への理解
- リリースに関するツールの理解
  - Capistrano
  - Ansible
