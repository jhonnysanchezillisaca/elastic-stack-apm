# Elastic stack with APM

- [Quick Run](#quick-run)
- [Maintenance](#maintenance)
- [Remarks](#remarks)
- [Resources](#resources)

elasticsearch apm-server logstash kibana

# Quick Run

```sh
docker-compose up -d
```
Give Kibana a few seconds to initialize, then access the Kibana web UI by hitting
[http://localhost:5601](http://localhost:5601) with a web browser and use the aforementioned credentials to login.

By default, the stack exposes the following ports:
* 5000: Logstash TCP input.
* 9200: Elasticsearch HTTP
* 9300: Elasticsearch TCP transport
* 5601: Kibana


Go to `localhost:5601`, or what your machine IP

Wait for kibana to be available, then you are ready to try apm

## Maintenance 
To delete older indexes using curator set up a cron or Jenkins job that runs `docker-compose run --rm curator --config config.yml action-file.yml`


# Remarks

- Since v6.4, apm dashboard setup move to Kibana UI.

  ![](https://github.com/yidinghan/eak/raw/master/images/apm-setup-instructions.jpg)
  ![](https://github.com/yidinghan/eak/raw/master/images/load-kibana-objects.jpg)

# Resources

- docker elastic: https://www.docker.elastic.co/
- elasticsearch

  - image: `docker pull docker.elastic.co/elasticsearch/elasticsearch:6.5.1`
  - github: https://github.com/elastic/elasticsearch
  - docker: https://www.elastic.co/guide/en/elasticsearch/reference/6.0/docker.html
  - vm.max_map_count: https://github.com/docker-library/elasticsearch/issues/111#issuecomment-268989731

  ```shell
  $ grep vm.max_map_count /etc/sysctl.conf
  vm.max_map_count=262144

  $ sysctl -w vm.max_map_count=262144
  ```

- apm-server
  - image: `docker pull docker.elastic.co/apm/apm-server:6.5.1`
  - github: https://github.com/elastic/apm-server
  - docker: https://www.elastic.co/guide/en/apm/server/current/running-on-docker.html
  - config: https://github.com/elastic/apm-server/blob/master/apm-server.reference.yml
- kibana
  - image: `docker pull docker.elastic.co/kibana/kibana:6.5.1`
  - github: https://github.com/elastic/kibana
  - docker: https://www.elastic.co/guide/en/kibana/6.0/docker.html
- apm agent
  - nodejs: https://www.elastic.co/guide/en/apm/agent/nodejs/current/intro.html
    - agent api: https://www.elastic.co/guide/en/apm/agent/nodejs/current/agent-api.html
    - github: https://github.com/elastic/apm-agent-nodejs
