# Solr-Cluster-Docker
Building solr cloud using docker and simple loadbalancer to solr nodes

* Configuration: 
    * Solr nodes : 3
    * Zookeeper nodes : 3
    * java version : 11
    * solr version : 8.11

# Running Solr
* run `mkdir solrcloud` to create project directory
* Go to project folder
    * run ` cd solrcloud`
* Create three solr data folders.These are used to mount as docker container volumes
* Create 3 data folders
    * run `mkdir solr1data`
    * run `mkdir solr2data`
    * run `mkdir solr3data`

* Place `docker-compose.yml` in `solrcloud` folder
* Docker compose using `docker compose up -d`

# Setup loadbalancer
* place `solr_loadbalancer.conf` in your project folder
* Add server to Ngnix 
    * Go to `nginx.conf` in Ngnix installation path
    * Go to last line in `http` key. it would resemble like below 
    ```json
    events {
        worker_connections  1024;
        }
    http {
            ...
            ...
            ...
        include /<project-path>/solrcloud/solr_loadbalancer.conf
    }

    ```
    * Place `include /<project-path>/solrcloud/solr_loadbalancer.conf` command as shown above 
    * reload config by `ngnix -s reload`

Now go to `http://mysolrcloud` you should be seeing Solr UI admin loaded.

-- Happy coding
<br>
-- Kasi Yeswanth
