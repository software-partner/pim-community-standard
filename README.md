Akeneo PIM Community Standard Edition
=====================================

Welcome to Akeneo PIM Product.

This repository is used to create a new PIM project based on Akeneo PIM.

If you want to contribute to the Akeneo PIM (and we will be pleased if you do!), you can fork the repository https://github.com/akeneo/pim-community-dev and submit a pull request.

Scrutinizer | Crowdin
----------- | -------
[![Scrutinizer Quality Score](https://scrutinizer-ci.com/g/akeneo/pim-community-dev/badges/quality-score.png?s=05ef3d5d2bbfae2f9a659060b21711d275f0c1ff)](https://scrutinizer-ci.com/g/akeneo/pim-community-dev/) | [![Crowdin](https://d322cqt584bo4o.cloudfront.net/akeneo/localized.svg)](https://crowdin.com/project/akeneo)

Application Technical Information
---------------------------------

The following documentation is designed for both clients and partners and provides all technical information required to define required server(s) to run Akeneo PIM application and check that end users workstation is compatible with Akeneo PIM application:
https://docs.akeneo.com/master/install_pim/manual/system_requirements/system_requirements.html

Installation instructions
-------------------------

### SWP specific installation

Clone repo and checkout development branch:

```
git clone git@github.com:software-partner/swp-akeneo-dev.git
cd swp-akeneo-dev
git checkout swp-development
git submodule init
git submodule update
```

Use  distributed configuration:

```
cp docker-compose.override.yml.dist docker-compose.override.yml
cp app/config/parameters.yml.dist app/config/parameters.yml
cp .env.dist .env
```

Startup containers:

```
docker-compose up -d
```

Make sure your GitHub token is provided (in composer configuration)

Run Akeneo installation scripts:

```
bin/docker/pim-dependencies.sh
bin/docker/pim-initialize.sh
```
Akeneo should now be reachable via http://localhost:8080/

Please check https://docs.akeneo.com/3.1/install_pim/docker/installation_docker.html


#### Dump production database

See https://devcenter.heroku.com/articles/jawsdb#backup-import-data-from-jawsdb-or-another-mysql-database

```shell script
mysqldump --column-statistics=0 -h OLDHOST -u OLDUSER -pOLDPASS OLDDATABASE > backup.sql

```

### Recommended installation

To install Akeneo PIM for a PIM project or for evaluation, please follow: https://docs.akeneo.com/master/install_pim/manual/installation_ce_archive.html

### Using Composer to create the project

Alternatively, you can install Akeneo PIM with Composer, but please make sure that all requirements are fulfilled.

If you don't have Composer yet, download it following the instructions on http://getcomposer.org/ or just run the following command:

```
    $ curl -s https://getcomposer.org/installer | php
```

Please note that you will certainly need to provide your GitHub credentials with this method.
A lot of our dependencies are coming from GitHub and this reaches the max limit of 50 API calls from anonymous users.

```
    $ php composer.phar create-project --prefer-dist akeneo/pim-community-standard ./pim-project "3.1.*@stable"
```

After that, follow the instructions here:

Manual: https://docs.akeneo.com/master/install_pim/manual/index.html
Docker: https://docs.akeneo.com/master/install_pim/docker/installation_docker.html

Upgrade instructions
--------------------

To upgrade Akeneo PIM to a newer version, please follow:
https://docs.akeneo.com/master/migrate_pim/index.html
