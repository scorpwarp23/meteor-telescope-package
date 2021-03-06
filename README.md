Meteor package for Telescope Application 
--------------------------------------------------------------------
Integrate the Telescope application within any Meteor Application

## Introduction
This is integration fork of [Meteor Telescope Application](https://github.com/SachaG/Telescope). Made it as meteorite atomosphere package, so that you can integrate it in your application within few minutes and voila !! you have Telescope applicaiton up and running without any new meteor instance or server instance.

Following are good thing about this package:
- Available as meteorite/meteor package
- Easily integrable in your application
- All the CSS are handled, so that it wont mess with your application
- Configurable site url for application 
- Made it to Bootstrap-3 compatible
- Works well with existing application accounts-ui authentication
- Improved post list page, improved search page showing which search results are being shown

## Requirement

While using this package, it requires following
- the application should use the iron router for rendering the templates and should have the default Iron Router 'layoutTemplate' for rendering its page
- application must use accounts-ui authentication for login, this packaged app do not have the login functionality, though it makes use of host application implemented accounts UI

##How to integrate with your application
Make sure that `node` and `npm` are installed.
### Install Meteorite
First you need to install `meteorite` npm package itself, using following command

`npm install -g meteorite` 

### Add to telescope package
It is meteorite package you need to install using folllowing command

`mrt add telescope-package`

Now, it will add the meteor-telescope to your package and its dependencies.

### Configure the packaged Telescope application 
After above installation is done, you need to configure application. It provides the following connfiguration
- Site URL
- Site Title
- Enable/Disble notifications across application
- Enable/Disable categories i.e tagging support for post
- Enable/Disable userlinks on post
- Change the backgroud color

For configuration, we exposed one object called `TelescopeConfig` and two functions called `telescopeRoutes` and `telescopeRoutesServer`, which are used for configuring the routes.
Typical way to put configuration in `Meteor.startup` method.

Following is **minimal configuration** to run the packaged telescope application, put following in `somefileName.js` file under `lib` or any top level directory other than `client` and `server`

Configuration of Site URL is must for package, so that configured telescope app available at `/<configured-root>`. i.e your host application will be available at `/` and packaged telescope application will be available at `/<configured-root>`

```

// congiguration of siteURL
TelescopeConfig.siteUrl='forum'

if(Meteor.isClient){
    Meteor.startup(function () {
      telescopeRoutes(TelescopeConfig.siteUrl);
    });
}

if(Meteor.isServer){
  Meteor.startup(function () {
    telescopeRoutesServer(TelescopeConfig.siteUrl);
  });
}

```

*Note. You must put above configuration, in order to run application.*

But you can do following following full configuration- properties are self explanatory

```
if(Meteor.isClient){
  Meteor.startup(function () {
    TelescopeConfig.title='My Site' 
      TelescopeConfig.siteUrl='forum'
      // Need to specify enablement of notifications, in server startup too
      TelescopeConfig.enableNotifications=true
      TelescopeConfig.enableUserLinks=true
      TelescopeConfig.enableCategories=true
      TelescopeConfig.backgroudColor='#353535'
      telescopeRoutes(TelescopeConfig.siteUrl);
   });
  }
 
 if(Meteor.isServer){
  Meteor.startup(function () {
    // Need to specify enablement of notifications, here too. if enabled in client
    TelescopeConfig.enableNotifications=true
    TelescopeConfig.siteUrl='forum'
    telescopeRoutesServer(TelescopeConfig.siteUrl);
  });
}

  ```
  
Following functionality is not provied as compared to Telescope application
- Nested comments which reply on the comment
- No markdown for posts and comment
- Sharing is not supported
- downvoting to comments
