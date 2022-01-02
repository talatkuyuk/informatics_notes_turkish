## Heroku Notları

#### Create an app
https://dashboard.heroku.com/apps
+ <New> button on RHS
+ Tap <Create new app>
+ App name must be unique
+ Choose a region
+ No need to add pipeline for now
+ Tap the button <Create app>
+ You can create the most 5 apps in free tier

#### An application settings
https://dashboard.heroku.com/apps/app-name
+ Open app: goes to app web site
+ More > View logs: you can see the app logs

**Resources:** 
+ As you see the expression **npm start**, your package.json needs to have *start script*
+ Dyno means simply *docker*
+ Add-ons can be a redis server, postgre server etc.

**Redis Add-on**
+ You should add your credit card for create redis add-on
+ Add the add-on following instructions
+ Heroku redis: settings > View Credentials

**Deploy:**
+ You can choose *deployment method*. For instance Github, Heroku git, or Container Registry
+ If you choose github, you must arrange your repo is visible by heroku.
+ All arrangments must be set for contiunes deployment

**Settings:**
+ Add config vars (value-key in .env file)
+ You can add SSL certificates
+ You can see your app domain created by heroku; or you set a custom domain