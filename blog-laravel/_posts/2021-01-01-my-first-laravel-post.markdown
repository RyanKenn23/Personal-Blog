---
layout: post
title:  "A simple laravel login system!"
date:   2021-01-01 12:13:44 +0300
category: laravel
image: /assets/images/wizard-login.jpg
---

_This is a website system where users create ,read and reply to articles.The users need to have an account and be logged in before they do anything in the website.The system was devepoled in visual studio code platform using laravel,html,css ,sql and javascript programming languages.Here are the steps i took to reach to project completion_:

1. Installing composer into my pc which helps in simplifying  the coding process when using laravel.It easily installs most of the dependancies you require in any project.You can get composer at [composer][comp].


2. Creating the project directory using the  composer in cmd , command:composer create projectname --prefer -dist laravel/laravel version of laravel you want for your project ,mine 8.THis creates the project directory with most dependancies ready for you to work with.Laravel uses the Model-view-Controller (MVC)structure.The model which is called the eloquent model is what interacts with the database on your behalf querrying it and giving you the results back.The view is where the user gets to see  and interact with your system,this is where you place your html code.THe css and javascript code  is placed in the public folder in your project directory.THe controller is where you place your system logic.Laravel also uses routes.Routes is a way of creating a request URL of your application. This is basically how  requests are mapped in your system.Each route has its own url and the associated controller to handle the request.Example is create article:Here i created a route which will display the create article view where the user will create the article. For my system's case since its a web application all routes are in the web.php folder.

3.  After creating my project folder  now its time to get to the coding process.For my case i needed views for creating ,displaying and replying to articles.My system needs a database to store the articles.For my case i am using phpmyadmin.You can get phpmyadmin by installing [Xampp][xam] in your system.On phpmyadmin i created a database which i  used in my system.Once i created the database in phpmyadmin i specified it in my laravel system so that it knows what database to use.You do that in the .env file.Next i created  tables for articles and replys.Laravel gives you a easier way of creating tables  by using migrations.To create a migration in your project directory in cmd run:php artisan make:migration create_articles_table.THis will create a migration file where you will be able to specify the table columns and the datatypes for the columns  inside the public funtion up.eg $table->string('title')->unique().The name of the column is title the datatype it stores is string and the unique function specifies tha each row should be unique,articles cannot have the same title.I did that for all the columns i needed in my system .After i specified all the columns i needed for my table the next step is to create it.I used the command:php artisan migrate.THis created the table articles with the columns i specified in the migration file.Next  a model is needed to interact with my  table.I  created a model in cmd in the project directory using the command:php artisan make:model Article.THe name of the model is article and the name should be similar to the table name.The table name is plural and the model name singular.In the model this where i speciied  relationships between the tables in my system eg an article has many replies but a reply belongs to an articles ie  
   " public function reply()
    {
        return $this->hasMany(Reply::class);
    }"
    This is  function is in the article model and it showcases the one to many relationship between articles and replies.All its saying is that for a particular article it has many replies hence(Reply::class).Any time you have an article and you run the reply method on it ,it will give you all the replies for that particular article.The same procedure is done for replies. 

4. Now since i have the tables and model ready next i created the views for my system.I needed a view for the homepage,creating an article ,displaying the articles and replying to an article.I created the views inside the resources/views folder.THe views have plain html in them.The css and javascript for my system  is in  the public directory of my  laravel project.To easen my work i created a layout view which contained basic layout for my site then for the other views i just used the layout view by including the command @extends('nameofmylayout') then i just added specific html to that view only.After creating the views the next step is to create the controllers.


5. Controllers is where the logic of your system is specified in laravel.To create a controller inside my project directory in cmd i ran the command:php artisan make:controller ArtriclesController.The name of the controller is ArtriclesController.Inside this controller is where i specified which view to be displayed and the methods to be executed in my system.I  also created the controller for replies and did  the same thing.  

6. Once done with the controllers i  headed over to  the routes directory and selected the web folder since my project is a website and all web routed should be loacated in that folder.Each request which will be made in my website must have an associated route .The structure of routes is as follows:Route::get('/articles', [ArticlesController::class,'index'])->name('articles.index').THis route will display the create article view.The url is '/articles' it uses the articlescontroller's method called  index and i named the route .I did this for all the routes in my system.Then in to link this routes .IN my homepage i have links like create article and i linked them to the articles routes.I did this for all the links i needed.

7. I tested out all my system so far and it was working as i intended.ONly one part was missing the authorization.Laravel uses auth to perform authorization in websites.To include auth in your system there a couple of commands you need to run,
        a) composer require laravel/ui --dev
        b) php artisan ui vue --auth 
   the last command will give you a command to run, run it and you are set.
   THis command will install all the dependancies you need to perform authization in your system.Since my website i created from scratch i included the laravel login links in my website.To limit use to only registered users i included ->middleware('auth') in all the relevant routes in my system .Now you cannot create,reply to or read articles without being registered .

   THat is how i achieved my login system. 
   _Here is the link to the code:  [loginsystem][log]_



 [comp]: https://getcomposer.org/
 [xam]: https://www.apachefriends.org/download.html
 [log]: https://github.com/RyanKenn23/laravel-login-system

