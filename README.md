Django-dynamic-scraper
===================

Django-dynamic-scraper use scrapy base on django framework and use admin django interface create scrapy crawl many website.

----------

## Requirements:



>  - Python 2.7+ or 3.4+
>  - Django 1.8/1.9
>  - Scrapy 1.1
>  - Scrapy-djangoitem 1.1
>  - Python JSONPath RW 1.4+
>  - Python future
>  - scrapyd
>  - django-celery
>  - django-dynamic-scraper



## Documents
-------------

[Tutorial DDS](https://django-dynamic-scraper.readthedocs.io)

[Scrapyd-client](https://github.com/scrapy/scrapyd-client)

[DjangoItem in scrapy](https://github.com/scrapy-plugins/scrapy-djangoitem)

## SETUP:

## 1. Install docker, compose

install docker
> wget -qO- https://get.docker.com/ | sh
sudo usermod -a -G docker `whoami`

 install compose
> sudo wget -q https://github.com/docker/compose/releases/download/1.6.2/docker-compose-`uname -s`-`uname -m` \
    -O /usr/local/bin/docker-compose
> sudo chmod +x /usr/local/bin/docker-compose

**Tip** : after that, logout, then login for update environment

---------

## 2. Run docker django-dynamic-scraper

- clone git onfta-crawler
> git clone git@gitlab.com:hv-db04/onfta-crawler.git
> cd onfta-crawler/django_dynamic_scraper

- run docker onfta-crawler
> docker-compose up -d
> docker exec -it <id container> bash

---------

## 3. Defining the object to be scraped




- create Database utf8
>  CREATE DATABASE news CHARACTER SET utf8 COLLATE utf8_general_ci;
> $cd djangoItem

- create user admin
>  python manage.py createsuperuser

- run django server
>  python manage.py runserver 0.0.0.0:8000

- show admin django in browser
>  http://localhost:8000/admin

> + add New Scraped object classes
> + add New Scrapers
> + add News websites

---------

## 4. run crawl data


> **run**:

**script:** ` scrapy crawl [--output=FILE --output-format=FORMAT] SPIDERNAME -a id=REF_OBJECT_ID [-a do_action=(yes|no) -a run_type=(TASK|SHELL) -a max_items_read={Int} -a max_items_save={Int} -a max_pages_read={Int} -a output_num_mp_response_bodies={Int} -a output_num_dp_response_bodies={Int} ] `

>  scrapy crawl news -a id=1 -a do_action=yes

-----------------------------
## 5. run schedule crawl:

>  **deploy project scrapy**:

> - cd crawl
> - scrapyd-deploy -p crawl
> - scrapyd

---------

> **run schedule scrapy**:

**script:** `python manage.py celeryd -l info -B --settings=example_project.settings`

> python manage.py celeryd -l info -B --settings=djangoItem.settings

---------
>**run check  error expath**:

**script:** `scrapy crawl news_checker -a id=ITEM_ID -a do_action=yes`
