FROM python:3.4-slim

RUN apt-get -y update && apt-get -y install libxml2 libxml2-dev libxslt-dev gcc mariadb-client \
  && pip install pytest \
  && pip install coverage \
  && pip install nose \
  && pip install nose-parameterized \
  && pip install lxml \
  && pip install isodate \
  && pip install pytz \
  && apt-get -y remove gcc \
  && apt-get -y autoremove \
  && apt-get -y clean

