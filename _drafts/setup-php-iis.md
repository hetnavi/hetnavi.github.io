---
layout: post
title: "Setup php in IIS"
excerpt_separator: <!--more-->
---

## install php

* php 8.0.9 (VS16 x64 Non Thread Safe) @ c:/php/php-`xxx`...
* Visual C++ Redistribute 2015-2019

## configure php

### edit php.ini

* fastcgi.impersonate = 1
* cgi.fix_pathinfo = ""
* cgi.force_redirect = 0

## install iis

* Settings
    * Turn Windows feature on or off
        * check Internet Information Services

## configure iis

### Server Manager

* Roles
    * Add Role Services
        * enable CGI

### Server

* FastCGI
    * Fullpath
        * C:/php/php-`xxx`/php-cgi.exe
    * InstanceMaxRequests
        * 10000
    * MaxInstances
        * 4
    * Environment Variables
        * PHP_FCGI_MAX_REQUESTS
            * 10000
* Handler Mapping
    * Add Module Mapping
        * Request path
            * *.php
        * Module
            * FastCgiModule
        * Executable
            * "C:\php\php-`xxx`\php-cgi.exe"
        * Name
            * PHP`xxx`_via_FastCGI
* Application Pool
    * .NET Framework version
        * No Managed Code
    * Managed pipeline mode
        * Integrated

### Site

* Map application pool
* Set DefaultDocument
    * index.php
