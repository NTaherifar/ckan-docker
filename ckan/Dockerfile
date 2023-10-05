FROM ckan/ckan-base:2.10.1
#FROM ckan/ckan-base:2.9.9

# Set up environment variables
ENV APP_DIR=/srv/app
ENV TZ=UTC
RUN echo ${TZ} > /etc/timezone

# Make sure both files are not exactly the same
RUN if ! [ /usr/share/zoneinfo/${TZ} -ef /etc/localtime ]; then \
        cp /usr/share/zoneinfo/${TZ} /etc/localtime ;\
    fi ;

### Spatial extension ###
RUN apk add python3-dev libxml2-dev libxslt-dev geos geos-dev proj proj-dev proj-util py3-shapely
RUN pip install --upgrade pip
RUN pip install -e "git+https://github.com/ckan/ckanext-spatial.git#egg=ckanext-spatial"
COPY spatial-reqs.txt /tmp/spatial-reqs.txt
RUN pip install -r /tmp/spatial-reqs.txt

### doi extension ###
RUN pip install ckanext-doi


COPY setup/start_ckan.sh.override ${APP_DIR}/start_ckan.sh
