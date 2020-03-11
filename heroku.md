sign up for a heroku account

brew install heroku/brew/heroku

heroku login
heroku: Press any key to open up the browser to login or q to exit
› Warning: If browser does not open, visit
› https://cli-auth.heroku.com/auth/browser/***

Heroku

install heroku
https://devcenter.heroku.com/articles/getting-started-with-nodejs?singlepage=true

create fake express app first express generator ‘jdrichardstech-express-test’
npm install
test app ‘nodemon’ you should see basic express app
set up gitignore with node_modules and .env
git init
do first git commit

create this inside the folder
heroku create [optional name] //use your name name cannot repeat any other name on the already used in heroku

git remote show
you will see (heroku)
if it is a github app as well you will also see origin

both can exist

now let’s push to heroku
git push heroku master

heroku open will open the app in the browser
your app is deployed

now with oshop app

connect database
dashboard -> resources -> mlabs mongodb -> sign up with credit but will be a sandbox so free

remember to create the CONFIG variables and explain
show the database

list of commands

https://devcenter.heroku.com/articles/heroku-cli-commands
