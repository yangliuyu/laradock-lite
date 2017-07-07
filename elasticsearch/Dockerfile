FROM docker.elastic.co/elasticsearch/elasticsearch:5.4.3

# For advanced usage please check here https://www.elastic.co/guide/en/elasticsearch/reference/5.4/docker.html

MAINTAINER Liu Yang <yangliul@gmail.com>

USER root

RUN yum install -y unzip

# install plugins
RUN wget https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v5.4.3/elasticsearch-analysis-ik-5.4.3.zip -O analysis-ik.zip
RUN mkdir plugins/analysis-ik && unzip analysis-ik.zip -d plugins/analysis-ik && rm analysis-ik.zip

RUN wget https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v5.4.3/elasticsearch-analysis-pinyin-5.4.3.zip -O analysis-pinyin.zip
RUN mkdir plugins/analysis-pinyin && unzip analysis-pinyin.zip -d plugins/analysis-pinyin && rm analysis-pinyin.zip

EXPOSE 9200 9300
