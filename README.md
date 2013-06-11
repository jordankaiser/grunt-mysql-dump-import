# grunt-deployments

> Push/pull MYSQL databases from one location to another using Grunt. Designed to ease the pain of migrating databases from one environment (local) to another environment (remotes). Automatically updates hardcoded siteurl references and backs up source and target before any modificaitions are made.

## Getting Started
This plugin requires Grunt `~0.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-deployments --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-deployments');
```

## The "deployments" task

### Overview
In your project's Gruntfile, add a section named `deployments` to the data object passed into `grunt.initConfig()`.

The task expects a series of `targets`, one for each of the locations which you want to move the database to/from.

You must define a `local` target.

```js
grunt.initConfig({
  deployments: {
    local: {
      
    },
    my_target_1: {
     
    },
    my_target_2: {
     
    },
    // etc
  }
});
```

**Please note:** The task is opinionated in that it assumes you are working on a local machine and pushing/pulling databases from/to that location. Thus it is imperative that you define a `local` target as part of your configuration.

### Usage

#### Local Target (required)
As above, the Plugin task is opinionated. It *expects* that you are working locally and pushing/pulling from/to that location. 

As a result, it is essential that you define a *single* target *without* an `ssh_host` parameter. This is typically named "local" for convenience.

```js
"local": {
  "title": "Local", 
  "database": "local_db_name",        
  "user": "local_db_username",
  "pass": "local_db_password",
  "host": "local_db_host",  
  "url": "local_db_url"
  // note that the `local` target does not have an "ssh_host"
},
```

The task will assume that this target is equivilant to your `local` environment. You can call it anything you wish but it ***must not*** have an `ssh_host` parameter.

#### Other Environment Targets
All other targets *must* contain a valid `ssh_host` parameter. 

```js
"develop": {
  "title": "Development", 
  "database": "development_db_name",        
  "user": "development_db_username",
  "pass": "development_db_password",
  "host": "development_db_host",  
  "url": "development_db_url" 
  "ssh_host": "ssh_user@ssh_host"  
},
"stage": {
  "title": "Stage", 
  "database": "stage_db_name",        
  "user": "stage_db_username",
  "pass": "stage_db_password",
  "host": "stage_db_host",  
  "url": "stage_db_url" 
  "ssh_host": "ssh_user@ssh_host"  
},
"production": {
  "title": "Production", 
  "database": "production_db_name",        
  "user": "production_db_username",
  "pass": "production_db_password",
  "host": "production_db_host",  
  "url": "production_db_url" 
  "ssh_host": "ssh_user@ssh_host"  
}
```

#### Full Usage Example

The structure below represents an typical usage example for the task configuration. Obviously you should replace the placeholders with your own database/environment configurations.

```js
grunt.initConfig({
  deployments: {
    options: {
      // any should be defined options here
    },
    // "Local" target
    "local": {
      "title": "Local", 
      "database": "local_db_name",        
      "user": "local_db_username",
      "pass": "local_db_password",
      "host": "local_db_host",  
      "url": "local_db_url"
      // note that the `local` target does not have an "ssh_host"
    },
    // "Remote" targets
    "develop": {
      "title": "Development", 
      "database": "development_db_name",        
      "user": "development_db_username",
      "pass": "development_db_password",
      "host": "development_db_host",  
      "url": "development_db_url" 
      "ssh_host": "ssh_user@ssh_host"  
    },
    "stage": {
      "title": "Stage", 
      "database": "stage_db_name",        
      "user": "stage_db_username",
      "pass": "stage_db_password",
      "host": "stage_db_host",  
      "url": "stage_db_url" 
      "ssh_host": "ssh_user@ssh_host"  
    },
    "production": {
      "title": "Production", 
      "database": "production_db_name",        
      "user": "production_db_username",
      "pass": "production_db_password",
      "host": "production_db_host",  
      "url": "production_db_url" 
      "ssh_host": "ssh_user@ssh_host"  
    }
  },
})
```


### Options

#### options.backup_dir
Type: `String`
Default value: `backups`

A string value that represents the directory path (*relative* to your Grunt file) to which you want your database backups for source and target to be saved prior to modifications.

You may wish to have your backups reside outside the current working directory of your Gruntfile. In which case simply provide the relative path eg: ````../../backups````.



## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
_(Nothing yet)_
