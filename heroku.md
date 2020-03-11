create fake express app first ‘yourname-express-test’
npm i
test app ‘nodemon’ you should see basic express app
set up gitignore with node_modules
git init
do first git commit

create this inside the folder
heroku create [optional name]

git remote show
you will see (heroku)

now let’s push to heroku
git push heroku master

\*\*\* note away from this exercise git -u will make you able to do git push without origin master

heroku open will open the app in the browser
your app is deployed

connect database
dashboard -> resources -> mlabs mongodb -> sign up with credit but will be a sandbox so free
