FROM docker.elastic.co/elasticsearch/elasticsearch:5.5.3

# For advanced usage please check here https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docker.html

MAINTAINER Liu Yang <yangliul@gmail.com>

ADD elasticsearch-analysis-ik-5.5.3.zip  /usr/share/elasticsearch/analysis-ik.zip
ADD elasticsearch-analysis-pinyin-5.5.3.zip  /usr/share/elasticsearch/analysis-pinyin.zip

USER root

RUN yum install -y unzip

# install plugins
#RUN wget https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v5.5.3/elasticsearch-analysis-ik-5.5.3.zip -O analysis-ik.zip
RUN unzip analysis-ik.zip -d plugins && rm analysis-ik.zip && mv plugins/elasticsearch plugins/analysis-ik

#RUN wget https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v5.5.3/elasticsearch-analysis-pinyin-5.5.3.zip -O analysis-pinyin.zip
RUN unzip analysis-pinyin.zip -d plugins && rm analysis-pinyin.zip && mv plugins/elasticsearch plugins/analysis-pinyin

EXPOSE 9200 9300
