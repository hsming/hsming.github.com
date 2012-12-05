---
layout: post
title: "Deploy your app to Heroku"
description: ""
category: 
tags: [Heroku]
---
{% include JB/setup %}

#### First:

	$ rails new myapp
	$ cd myapp
I konw all this you done well. So let's begin here.

#### 1.Since Heroku provides you a PostgreSQL database for your app, edit your "Gemfile" and change this line:

	gem 'sqlite3' 
to this: 

	group :development, :test do
 	  gem 'sqlite3'
	end
	group :production do
      gem 'pg'
	end

then :

	$ bundle install

#### 2.Store your app in Git：
<br />
like this:

	$ git init 
	$ git add .
	$ git commit -m 'first commit'

#### 3.Deploy your app to Heroku
Create the app on Heroku:


	$ heroku create my_app
Deploy your code:

	$ git push heroku master

#### 4.Now, your app may work already. Or it show you "We are sorry, but something went wrong". Don't worry, just relax, You’ll need to run your database migrations.

	$ heroku run rake db:migrate

#### 5.Don’t forget to restart your application or you may cann't see any changes:

	$ heroku restart

Now open your Heroku site in your default web browser:

	$ heroku open
Your app will be running at http://my_app.herokuapp.com         ^_^

#### 6.Getting more help:
<https://devcenter.heroku.com/articles/rails3>

<http://railsapps.github.com/rails-heroku-tutorial.html>

If you got the error when you push your app to heroku like this:

	Permission denied (publickey).
	fatal: The remote end hung up unexpectedly
You can try :

	$ heroku keys:add

It may work sometimes, through i don't know the reason really.