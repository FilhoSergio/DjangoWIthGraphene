# 1º Stage
FROM registry.geomk.com.br/python_geomk/3.6-dev as builder
ENV PYTHONUNBUFFERED 1

RUN apk update && \
    apk add --no-cache \
        pcre-dev \
        linux-headers \
        python-dev \
        postgresql-dev \
        zlib

RUN pip install --upgrade pip && \
    pip wheel -w /requirements/whl \
    Django==1.10.2 \
    django-autocomplete-light==3.2.1 \
    django-autoslug==1.9.3 \
    django-colorfield==0.1.14 \
    django-cors-headers==2.0.2 \
    django-extensions==1.7.4 \
    django-filter==0.15.3 \
    django-fsm==2.6.0 \
    django-jsonfield==1.0.1 \
    django-modelwithlog==1.0.1 \
    django-ordered-model==1.3.0 \
    django-rest-swagger==2.1.0 \
    django-threadlocals==0.8 \
    djangorestframework==3.5.1 \
    djangorestframework-filters==0.9.1 \
    jsonfield==2.0.2 \
    oauthlib==0.6.0 \
    Pillow==5.1.0 \
    psycopg2==2.7.3 \
    psycopg2-binary==2.7.4 \
    pycpfcnpj==1.0.2 \
    Pygments==2.1.3 \
    requests==2.18.4 \
    whitenoise==3.3.1 \
    uwsgi==2.0.17 

# 2º Stage
FROM registry.geomk.com.br/python_geomk/3.6-prd
ENV VERSION v1.2.1
# Packages required

RUN apk update && \
    apk add --no-cache \
    pcre

COPY --from=builder /requirements/whl /requirements/whl
RUN pip install /requirements/whl/* && rm -rf /requirements

COPY --chown=82:82 ./source /source

RUN set -x \
    && addgroup -g 82 -S www-data \
    && adduser -u 82 -D -S -G www-data www-data

USER www-data


# RUN python /source/manage.py collectstatic --no-input -v 0

WORKDIR /source