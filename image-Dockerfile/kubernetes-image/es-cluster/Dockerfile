FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.3.0

COPY --chown=elasticsearch:elasticsearch ./config/ /usr/share/elasticsearch/
COPY --chown=elasticsearch:elasticsearch  ./config/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml
COPY ./analysis-ik-6.3.0/ /usr/share/elasticsearch/plugins/ik/

RUN yum -y install bzip2
COPY elasticsearch-head-master-docker.tar.gz /usr/share/elasticsearch/
RUN cd /usr/share/elasticsearch/
RUN tar zxvf elasticsearch-head-master-docker.tar.gz
RUN yum install -y epel-release 
RUN yum install -y npm nodejs wget bind-utils

EXPOSE 9100 9200 9300
COPY  docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
COPY  run-elasticsearch-head.sh /usr/local/bin/

RUN wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64" \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true
USER elasticsearch
ENTRYPOINT ["docker-entrypoint.sh"]
