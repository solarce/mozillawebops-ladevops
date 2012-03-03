# Web Apps!

* Typically Django
* Apache / mod_wsgi
* Usually MySQL

# Other Services

* Often Memcache and ElasticSearch
* Sphinx for older ones
* Generally using RabbitMQ to feed tasks to Celery worker queue
* Newer apps made use Redis

# Infrastructure

* dev/stage/prod
* everything load balanced
* services are built in clusters

# Clusters

 * generic clusters for smaller apps
 * dedicated clusters for some larger apps
 * admin node

# Admin node is

 * where code updates are pulled to
 * where deploys are done from

# Example Architecture

* DIAGRAM HERE

# How a deploy works

* app code is in ```/data/{dev|stage|prod}/src/site/code```
* since most our apps are open source, certain settings file aren't in
  public repos
* update script, typically bash

# Update script

 * git pull
 * update vendor submodule
 * any admin tasks, like compressing assets, database migrations
 * code is rsync'd to /data/{dev|stage|prod}/www/ , rsync strips out .git, .hg, etc
 * once code is rsync, it's checked into an internal git repo to keep revision of non-public files
 * deploy script (fabric code) is called which kicks off a pull on each web server
 * once all the web server pulls have kicked off, script exits
 
# Example Deploy output
 
* example run on https://gist.github.com/0049ca9c4e37d4f06da7

# What's next?

* continuous delivery
* internal paas
* vagrant
* community it

# continuous delivery?

* driven by jenkins?
* unit/integration tests as part of deploy
* phased rollouts

# Internal PaaS?

 * CloudFoundry?
 * Stackato?
 
# Vagrant

* some webapps already ship with Vagrantfiles
* provide Vagrantfiles for every cluster/webapp

# Community IT

 * http://blog.mozilla.com/mrz/2012/01/30/mozilla-it-growing-community/
 * Opening up some of our internal configs, code, etc

# Stuff to share
  
  * Puppet code (modules/manifests/etc)
  * Yum Repos
  * Deploy Scripts
  * One Click Deploy WebApps (commander, chief, freddo)

# Questions?