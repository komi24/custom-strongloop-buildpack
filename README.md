# StrongLoop Buildpack for Heroku 

StrongLoop provides:
 * LoopBack, an open-source Node.js framework that enables you to create dynamic end-to-end REST APIs with little or no coding. For more information on LoopBack, see http://loopback.io.
 * StrongLoop Controller, a Node devops system.  See [StrongLoop Controller docs](http://docs.strongloop.com/display/SLC/StrongLoop+Controller) for more information.
 * StrongLoop Agent (StrongOps), an operational console for Node.js applications that provides deep performance monitoring including CPU profiling, event loop statistics, and more.  See [StrongLoop Agent docs](http://docs.strongloop.com/pages/viewpage.action?pageId=3834736) for more information.

Follow the steps in <a href="http://docs.strongloop.com/display/SLC/Getting+started+with+StrongLoop+Controller">Getting started</a> to install Node and the StrongLoop command-line tool, then create a StrongLoop application on your local system using the <a href="http://docs.strongloop.com/display/LB/Create+a+simple+API">slc loopback</a> command.

Then follow the steps below to deploy the app to Heroku.

## Create Procfile and commit 

1. Create a Procfile in the root directory of your app that contains the following:  web: slc run
2. Update package.json to use the latest stable version of node.
    
        {
            "engines": {
                "node": "0.10.x"
            }
        }

3. To deploy, add your application to a Git repository.
 
        $ git init
        $ git add -A
        $ git commit -a -m "Initial Commit"

Note : For faster deployment time, delete the application's node-modules directory.


## Push to Heroku

The StrongLoop Heroku add-on provisions a monitoring account on StrongOps.

If you haven't already done so, register an account on Heroku. 
Install the Heroku Toolbelt.
Login with the Heroku command line: 

    $ heroku login

Once you are ready to deploy your app, follow these steps:

1. Create your Heroku app using the StrongLoop buildpack with the first command below.  When it completes, push to Heroku master to complete the installation of the node and the strongloop cli tools on your dyno.

        $ heroku apps:create --buildpack https://github.com/strongloop/strongloop-buildpacks.git
        $ git push heroku master

1. Test it with this command:
   
        $ heroku open

## Check your dashboard on Heroku

Once you have created your app, it's time to look at the instrumentation.

1. Go to **Heroku** and find your app. 
2. Click **Heroku app dashboard** to view the various dynos and add-ons for your app. 
3. Select **StrongLoop add-on** to enable StrongOps monitoring. 
4. Click **StrongOps Dashboard** to access the StrongLoop Ops dashboard.

## Run your app in clustered mode through Heroku

Update the start command in the Procfile:

    $ web: slc run --cluster n 


Commit your changes and redeploy the app:

    $ git add Procfile
    $ git commit -m "Started clustered app" Procfile
    $ git push heroku master

Once you have set this up, you can control the cluster through the StrongLoop dashboard.

1. Go to Heroku and find your app. 
2. Click Heroku app dashboard to view the various dynos and add-ons for your app. 
3. Click StrongLoop add-on to view the StrongOps Control Panel. 
4. Click  StrongOps Dashboard to access the StrongLoop Ops dashboard.
5. Click on the Cluster tab to control your cluster. 


## Collect metrics for your app using StrongLoop Agent 

Update the start command in the Procfile:

    $ web: slc run --metrics STATS

Commit your changes and redeploy the app:

    $ git add Procfile
    $ git commit -m "Collect metrics using strong-agent" Procfile
    $ git push heroku master

For more information on how to use StrongLoop Agent API, refer to <a href="http://docs.strongloop.com/display/SLA/Using+third-party+consoles">Using third-party consoles.</a>





 






