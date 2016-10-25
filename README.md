Heroku buildpack for CommandBox [![Build Status](https://travis-ci.org/Ortus-Solutions/heroku-buildpack-commandbox.svg)](https://travis-ci.org/Ortus-Solutions/heroku-buildpack-commandbox)
=========================

This is the Heroku/Dokku buildpack for CommandBox

## How it works

The buildpack will allow you to deploy your CFML applications directly to Heroku (or to Dokku-enabled hosts) using CommandBox to manage your CFML engine.  It allows you to specify your custom server configuration settings using the CommandBox server API, avoiding additional script and configuration files during the Heroku deployment process.

## Usage

While both [Heroku](https://www.heroku.com/) and [Dokku](http://dokku.viewdocs.io/dokku/) proxy their traffic through NGINX, all files, including static assets, in your app will be served by the underlying Commandbox servlet container and the assigned CFML engine.  As such, deployments with this build pack are primarily targeted towards low to medium traffic sites.   Use cases include staging sites, bug logs, and system monitors and middleware apps which provide service to other applications in your stack.  

For more robust, high-traffic deployments consider using a customized buildpack using Tomcat behind Apache or NGINX.

Deploy a sample app:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Configuration

Below are the configuration options for both Heroku and Dokku environments.

### Heroku Configuration

Create your heroku app:

```
heroku apps:create myapp.mydomain.com
```

Heroku will return two URLS  - the app domain ( you can configure a custom domain later ), and the heroku repository remote url which is configured to deploy your application.

Set up a new remote for this url:

```
git remote add heroku https://git.heroku.com/myapp.mydomain.com.git
```

Set your buildpack for Heroku with the command

```
heroku buildpacks:set https://github.com/ortus-solutions/heroku-buildpack-commandbox.git
```

### Dokku Configuration

Create a file in the root of your project named .buildpacks and add the following to that file:

```
https://github.com/ortus-solutions/heroku-buildpack-commandbox.git
```

Now configure a new Git remote for your Dokku deployment ( Dokku will create the repo automatically if it doesn't exist ):

```
git remote add dokku https://dokku.mydomain.com/myapp.mydomain.com.git
```


## Deployment

Both Heroku and Dokku use a git push to the repository to trigger deployment.  By default the master branch is the only branch triggered for deployment with a push.  A simple push the repository triggers the deployment (using the remote name you set in configuration):

```
git push heroku master
```

You may override this by specifying a branch in your push to act as master (e.g. - deploying to a staging instance):

```
git push heroku yourbranch:master
```

Note:  Once deployment is returned as successful, you may receive NGINX 502 errors for up to 60 seconds as the CommandBox server starts up for the first time.


## LICENSE
Apache License, Version 2.0.

<hr/>

#### HONOR GOES TO GOD ABOVE ALL
Because of His grace, this project exists. If you don't like this, then don't read it, its not for you.

>"Therefore being justified by faith, we have peace with God through our Lord Jesus Christ:
By whom also we have access by faith into this grace wherein we stand, and rejoice in hope of the glory of God.
And not only so, but we glory in tribulations also: knowing that tribulation worketh patience;
And patience, experience; and experience, hope:
And hope maketh not ashamed; because the love of God is shed abroad in our hearts by the 
Holy Ghost which is given unto us. ." Romans 5:5

#### THE DAILY BREAD
 > "I am the way, and the truth, and the life; no one comes to the Father, but by me (JESUS)" Jn 14:1-12
