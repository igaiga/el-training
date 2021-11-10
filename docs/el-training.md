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
  - Please submit the URL of your GitHub repository on Google classroom. Everyleaf curriculum is long, so we will code review the merged PRs along the way. Also, if you wait for the review, it will be hard to get it reviewed, so you can keep merging without review.
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

### Step 10: Write the tests.

- TODO: Add igaiga text
- Get ready to write specs!
  - Prepare `spec/spec_helper.rb` and `spec/rails_helper.rb`.
- Let's write a model spec for validation
  - We won't actually write many validation tests, but let's try to get a better understanding of the model spec.
- Let's try writing a system spec for a task function.
- ~~Connect RSpec to GitHub Actions and have it send notifications to your channel on Discord.~~
  - You don't have to do this issue.
- Reference books for those who want to learn more:
  - English: https://leanpub.com/everydayrailsrspec
  - Japanese: https://leanpub.com/everydayrailsrspec-jp

### Step 11: Let's make the Japanese part of our app common

- Let's use the i18n mechanism in Rails to output validation error messages in Japanese or Nepalese.

### Step 12: Let's set the timezone for Rails

- Let's set the timezone for Rails to Japan Standard Time (Tokyo, JST) or Nepal Standard Time (NST).

### Step 13: Sort the task list by created_at.

- The tasks are currently sorted by ID, but let's try to sort them by created_at in descending order.
- Let's write a system spec to show that the sorting is working.

### Step 14: Let's Deploy

- Now that we have a simple task management system in our master branch, let's deploy it.
- Let's try to deploy to Heroku.
  - If you don't have an account, create one.
- Let's try to touch the deployed application on Heroku.
  - From now on, let's register tasks to this application and proceed with development.
  - However, since Heroku applications can be accessed anywhere on the Internet, make sure you don't post any information that you don't want to make public.
    - You may want to add basic authentication at this point.
  - From now on, you should continuously deploy your application to Heroku after each step.
- Describe how to deploy in `README.md`.
  - It would be better if you include the version information of the framework you are using in this app.

### Step 15: Add a due date

- Let's add an expiration date to a task.
- Let's make it possible to sort by due date in the list view.
- Let's expand the spec.
- Let's release it.

### Step 16: Let's add statuses and make them searchable.

- Let's add some statuses (not started, in progress, completed).
  - Optional: If you are not a beginner, you can install a gem to manage states.
- Let's make it possible to search by title and status in the list screen.
  - Optionally, if you are not a beginner, you can introduce a Gem that makes the implementation of search more convenient, such as ransack.
    - igaiga: I would recommend not using Ransack.
- When you narrow down the search, check the log to see the changes in the SQL issued.
  - Make it a habit to check this in the following steps as necessary.
- Attach a search index.
  - Prepare a slightly larger amount of test data, check the log/development.log, and confirm that the speed is improved by adding the index.
  - Optionally, you can use PostgreSQL's explain to check the index usage on the database side.
- Let's add a model spec to the search (system spec should also be expanded).

### Step 17: Set priorities

- Let's make it possible to register a priority (high, medium, low) for tasks.
- Let's make it possible to sort by priority.
- Expand the system spec
- Let's release it (and continue)

### Step 18: Add pagination

- Let's try to add pagination to the list screen using the Kaminari gem.

### Step 19: Apply the design.

- Let's install Bootstrap and apply the design to the app we've created so far.
  - Optionally, you can write your own CSS to design it.

### Step 20: Let's create a user model

- Let's create a user model.
- Let's create the first user with seed.
- Let's make sure that the first user created with seed is associated with a task.
  - Add DB index the relation.
  - When deploying to Heroku, please make sure that the tasks and users are already registered (data maintenance).

### Step 21: Let's implement the login/logout function.

- Let's try to implement it by ourselves without using any additional gem.
  - By not using Devise or any other Gem, the goal is to gain a better understanding of how HTTP cookies and Sessions work in Rails.
  - We also aim to deepen our understanding of authentication in general (e.g. password handling).
- Let's implement the login screen.
- If you are not logged in, you should not be able to go to the task management page.
- When a task is created, it should be associated with the user who is logged in.
- Show Only Tasks Created by You
- Let's Implement the Logout Function

### Step 22: Let's implement a user management screen.

- Let's add an administration menu on the screen.
- Make sure to prefix the admin screen with the URL `/admin`.
  - Before adding to `routes.rb`, let's design the URL and routing name (the name that will become `*_path`) in advance.
- Implement user list, create, update, and delete.
- When a user is deleted, the user's tasks will be deleted.
- Display the number of Tasks a User has in the User index page.
  - Let's introduce a mechanism to avoid the N+1 problem.
- Let's try to see the list of Tasks created by a User.

### Step 23: Let's add roles to users.

- Let's distinguish between administrative users and general users.
- Let's make it so that only administrative users can access the user management screen.
  - Raise a special exception when a normal user accesses the administration screen.
  - Supplement the exception with an appropriate error page (you can do this in step 25)
- Make it possible to select roles in the user management screen.
- Control the deletion of administrative users so that no one is left behind.
  - Let's use model callbacks.
- You are free to use or not use Gem.

### Step 24: Let's make it possible to label tasks.

- Let's add multiple Labels to Tasks.
- Let's try to search by Label.

### Step 25: Let's set up the error page properly.

- Let's take the default error page that Rails provides and turn it into a page of our own making.
- Configure the error page appropriately for your situation.
  - At least two types of status codes, 404 and 500, should be required.

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
