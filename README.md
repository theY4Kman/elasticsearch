## Elasticsearch Dockerfile


This repository is a fork of the official elasticsearch, except instead of using an automated pre-built versioned package of Elasticsearch, it uses Maven to build the latest master (at time of writing, 2.0.0-SNAPSHOT).


### Base Docker Image

* [dockerfile/java:oracle-java8](http://dockerfile.github.io/#/java)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Download [automated build](https://registry.hub.docker.com/u/they4kman/elasticsearch/) from public [Docker Hub Registry](https://registry.hub.docker.com/): `docker pull they4kman/elasticsearch`

   (alternatively, you can build an image from Dockerfile: `docker build -t="they4kman/elasticsearch" github.com/they4kman/elasticsearch`)


### Usage

    docker run -d -p 9200:9200 -p 9300:9300 they4kman/elasticsearch

#### Attach persistent/shared directories

  1. Create a mountable data directory `<data-dir>` on the host.

  2. Create Elasticsearch config file at `<data-dir>/elasticsearch.yml`.

    ```yml
    path:
      logs: /data/log
      data: /data/data
    ```

  3. Start a container by mounting data directory and specifying the custom configuration file:

    ```sh
    docker run -d -p 9200:9200 -p 9300:9300 -v <data-dir>:/data they4kman/elasticsearch /elasticsearch/bin/elasticsearch -Des.config=/data/elasticsearch.yml
    ```

After few seconds, open `http://<host>:9200` to see the result.
