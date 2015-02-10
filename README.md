Proclamer : Manifest Generator
============================
A very simple php script that generates a appcache manifest for websites based on the content of the directory



Install
-------

Download the zip and unzip it in a directory

create an appcache.json file containing your configuration in your project path

That's you'll have to do !

Usage
-----

Proclamer can be used by the command line , soon using http request

    $ php proclame.php
    Usage    : php proclame.php PROJECTPATH [CONFPATH] 
     
    Startup : 
        PROJECTPATH : your project directory where the website is stored 
        CONFPATH    : path to the config file appcache.config, relative to the current directory 
                      default : appcache.json in your project path 
Example use

    $ php proclame.php /www/site/
    

Configuring Proclamer
---------------------

Proclamer can be configured using an appcache.json file in your project directory

example of `appcache.json`

    $ cat appcache.json
    {
        "exclude":["system/", 
                    "application/",
                    "uploads/", 
                    "sql/", 
                    ".git/",
                    "composer.json",
                    "readme.md",
                    "license.txt",
                    ".htaccess", 
                    "*.php", 
                    "*.map"],
        "include":["/"],
        "network":["/api"],
        "fallback":[{"url":"/","fb":"fallback.html"},
                    {"url":"/api","fb":"api.json"}],
        "manifest":"manifest.appcache"
    }



Excluding Files
--------------

By default `proclame` will include all the files of your project directory except the manifest file and the configuration file

To exclude more files or directories, edit the `appcache.json` in your project path and add them in the `exclude` section

    "exclude":["system/"]         => Exclude all the system directory in your project root
    "exclude":["system"]          => Exclude all the files containing system in their names
    "exclude":["*.php"]           => Exclude all php files
    "exclude":["system/","*.php"] => Exlude the system directory and php files

Including URLs
---------------

Sometimes you will have to include a specific URL in your `CACHE` section that does not match with your project directory organisation

For example : `/` or `https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js`

The `include` group in `appcache.json` allows you to add those specific URLs in your `CACHE` section 

    "include":["/"] => include the root directory of your web site, usually index.html or index.php
    "include":["https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"] => include jquery


Configuring the NETWORK section
------------------------------

You'll want to tell the browser to load specific resources from the web using the `NETWORK` section

The `network` group in `appcache.json` allows you to add those specific paths in your `NETWORK` section 

    "network":["/api"] => Load the api from the server

By default `proclame` will add a wildcard as default value for the `NETWORK` section:

    NETWORK:
    *


Configuring the FALLBACK section
--------------------------------

You'll want to tell the browser to load specific resources if some paths are not accessible using the `FALLBACK` section

The `fallback` group in `appacache.json` allows you to add those specific paths and their fallbacks in your `FALLBACK` section 

    "fallback":[{"url":"/","fb":"fallback.html"}] => Load fallback.html if the website is inaccessible


Changing the manifest filename
------------------------------

You'll want to cutomize the `manifest.appcache` filename. It's up to you !

The `manifest` parameter in `appacache.json` allows you to customize the name of the generated file 

    "manifest":"iamcharlie.appcache" => change the manifest name to iamcharlie.appcache

Issues
------

If you have any issues using `proclame` or features you require, then please
file a bug https://github.com/lagaisse/ProclamerManifestGenerator/issues.

License
-------

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Licence Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/80x15.png" /></a>

