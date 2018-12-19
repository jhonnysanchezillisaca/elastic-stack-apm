FROM docker.elastic.co/elasticsearch/elasticsearch:6.5.1

ARG VERSION=6.5.1-23.2

RUN bin/elasticsearch-plugin install -b https://search.maven.org/classic/remotecontent?filepath=com/floragunn/search-guard-6/$VERSION/search-guard-6-$VERSION.zip

FROM docker.elastic.co/elasticsearch/elasticsearch:6.5.1
USER root
WORKDIR /usr/share/elasticsearch/

ENV ES_HOSTNAME localhost
ENV ES_PORT 9200

RUN chown elasticsearch:elasticsearch config/elasticsearch.yml
RUN chown -R elasticsearch:elasticsearch data
# install security plugin

ARG VERSION=6.5.1-23.2

RUN bin/elasticsearch-plugin install -b https://search.maven.org/classic/remotecontent?filepath=com/floragunn/search-guard-6/$VERSION/search-guard-6-$VERSION.zip
COPY ./safe-guard/install_demo_configuration.sh plugins/search-guard-5/tools/
RUN chmod +x plugins/search-guard-5/tools/install_demo_configuration.sh && ./plugins/search-guard-5/tools/install_demo_configuration.sh -y


USER elasticsearch

EXPOSE 9200