# MyHero - Docker Stack deployment

Following the amazing job done by "Hank Preston (https://github.com/hpreston)"
I've only integrated that in Docker stack deployment

## Myhero

Myhero is a Vote Processing Service for a basic microservice demo application.
This service subscribes to an MQTT Server where votes are waiting for processing.

* MyHero Demo - [hpreston/myhero_demo](https://github.com/hpreston/myhero_demo)

The application was originally designed to provide a simple demo for Cisco Mantl.  It is written as a simple Python Flask application and deployed as a docker container.

## Environmental Requirement

* docker
* docker-compose
* docker swarm

## Docker

The docker containers used are

* Data - [hpreston/myhero_data](https://hub.docker.com/r/hpreston/myhero_data)
* App - [hpreston/myhero_app](https://hub.docker.com/r/hpreston/myhero_app)
* Web - [hpreston/myhero_web](https://hub.docker.com/r/hpreston/myhero_web)
* UI - [hpreston/myhero_ui](https://hub.docker.com/r/hpreston/myhero_ui)
* Ernst - [hpreston/myhero_ernst](https://hub.docker.com/r/hpreston/myhero_ernst)
* Spark Bot - [hpreston/myhero_spark](https://hub.docker.com/r/hpreston/myhero_spark)
* Tropo App - [hpreston/myhero_tropo](https://hub.docker.com/r/hpreston/myhero_tropo)
* Mosca - [matteocollina/mosca](https://hub.docker.com/r/matteocollina/mosca)

# Environment 

## Configuration

* `cp docker-stack.yml.sample docker-stack.yml`
* `vi docker-stack.yml # edit the file and add your settings`

## Installation

* `./setup`

# Basic Usage

* http://PUBLIC IP:10301 (web)
* http://PUBLIC IP:10401 (ui)
* Cisco Spark and the associated Room 
* Tropo via the associated phone number

# Alternate and Advanced Configurations

Thanks to check on my hero portal: 

* https://github.com/hpreston/myhero_demo
* https://hub.docker.com/u/hpreston/

# Validation

* Data
  * `curl http://localhost:10101/hero_list`
* App
  * `curl http://localhost:10201/hero_list`
* Web
  * `curl http://localhost:10301/hero_list`
* UI
  * `curl http://localhost:10401/hero_list`

* Place a vote for an option
  * `curl http://localhost:10x01/vote/<HERO>`

New v2 APIs
These newer APIs require authentication as well as support more features

* Get the current list of options for voting
  * `curl -X GET -H "key: APP AUTH KEY" http://localhost:5000/options`
* Add a new option to the list
  * `curl -X PUT -H "key: APP AUTH KEY" http://localhost:5000/options -d '{"option":"Deadpool"}'`
* Replace the entire options list
  * `curl-X POST -H "key: APP AUTH KEY" http://localhost:5000/options -d @sample_post.json`
  * Data should be of same format as a GET request
* Delete a single option from the list
  * `curl -X DELETE -H "key: APP AUTH KEY" http://localhost:5000/options/Deadpool`
* Place a Vote for an option
  * `curl -X POST -H "key: APP AUTH KEY" http://localhost:5000/vote/Deadpool`
* Get current results
  * `curl -X GET -H "key: APP AUTH KEY" http://localhost:5000/results`

# Services

``` bash
# docker service ls
ID            NAME          MODE        REPLICAS  IMAGE
55sw6ikxdg00  myhero_data   replicated  3/3       hpreston/myhero_data:latest
jua8uv15qmd2  myhero_ernst  replicated  2/2       hpreston/myhero_ernst:latest
l42dlthi94df  myhero_app    replicated  3/3       hpreston/myhero_app:latest
qpjw5dkwet55  myhero_web    replicated  1/1       hpreston/myhero_web:latest
rawar1xhl6m5  myhero_mosca  replicated  2/2       matteocollina/mosca:latest
rxi7s21q15g2  myhero_tropo  replicated  1/1       hpreston/myhero_tropo:latest
uob06vjbsq2a  myhero_ui     replicated  1/1       hpreston/myhero_ui:latest
xjgsa12lblr5  myhero_spark  replicated  1/1       hpreston/myhero_spark:latest
```


