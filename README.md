### Code Status
[![Build Status](https://travis-ci.org/sidlinux22/ToDoAPP.svg?branch=master)](https://travis-ci.org/sidlinux22/ToDoAPP)

#### Ruby on Rails app
* ruby 2.0.0p481 (2014-05-08 revision 45883) [universal.x86_64-darwin13]

#### Configure/Create TOdo application:
<pre> rails new ToDoAPP </pre>

<pre>
  gem 'haml'
  gem 'bootstrap-sass', '~> 3.2.0.0'
  gem 'simple_form'
  gem 'sprockets', '=2.11.0'
  gem 'rails', '4.1.1'
  gem 'sqlite3'
  gem 'sass-rails', '~> 4.0.3'
  gem 'uglifier', '>= 1.3.0'
  gem 'coffee-rails', '~> 4.0.0'
  gem 'jquery-rails'
  gem 'sdoc', '~> 0.4.0',          group: :doc
  gem 'spring',        group: :development
</pre>

#### Deployment instructions
<pre>
cd ToDoAPP
bundle install
</pre>

* Database engine SQLite database engine
<pre>
adapter: sqlite3
database: db/development.sqlite3
</pre>

#### Model TASK
<pre>
tile: task's tile
      note: task's note
      completed: task's completed date 
</pre>

#### Create Model
<pre>
 rails generate model Task title:string note:text completed:date 
</pre>

* Database initialization
* SQLite database engine
* Apply model migration

<pre>
rake db:migrate RAILS_ENV=development 
</pre>

#### Create task (within rails console)

<pre>
Task.create(title: 'Sid task',  note: 'test task created')
rb(main):001:0> Task.create(title: 'Sid task',  note: 'test task created')
 (0.1ms)  begin transaction
SQL (1.3ms)  INSERT INTO "tasks" ("created_at", "note", "title", "updated_at") VALUES (?, ?, ?, ?)  [["created_at", "2014-12-11 06:01:48.226085"], ["note", "test task created"], ["title", "Sid task"], ["updated_at", "2014-12-11 06:01:48.226085"]]
(0.8ms)  commit transaction
task = Task.first
Task Load (0.2ms)  SELECT  "tasks".* FROM "tasks"   ORDER BY "tasks"."id" ASC LIMIT 1
=> #
:1
</pre>

<pre>
irb(main):005:0> task.save
(0.1ms)  begin transaction
(0.1ms)  commit transaction
=> true
</pre>

#### View
* application.html.haml
<pre>
!!!
%html
%head
  %title TOdo
  = stylesheet_link_tag "application", media: "all"
  = javascript_include_tag "application"
  = csrf_meta_tags
%body
  .row-fluid
    .span10.offset1
      .hero-unit.text-center
        %h1
          TOdo
        %p  TOdo APP
      = link_to 'New task', new_task_path, class: 'btn btn-primary'
  = yield
</pre>

* app/views/pages/home.html.haml

<pre>
.container
- if @tasks.empty?
  %span.text-warning There are no task!
- else
  %table.table.table-hover.table-bordered
    %thead
      %tr
        %th Title
        %th Create at
        %th Completed
  %tbody
    - @tasks.each do |task|
      %tr
        %td
          %strong= task.title
        %td.text-info= task.created_at
        %td.text-success= task.completed
#modal.modal.fade
</pre>

* application.css.scss
<pre>
@import  "bootstrap";
</pre>

#### Start Server

<pre>
rails server -p 3023 
</pre>

#### Loading app from browser

![alt tag](https://github.com/sidlinux22/ToDoAPP/blob/master/log/image.png)
