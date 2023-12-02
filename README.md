# ActualBudget with SimpleFin Sync
This project is made to simplify the setup of a dockerized version of ActualBudget with included bank syncing courtesy of SimpleFin.

When properly setup, it will run ActualBudget locally with a SimpleFin sync that runs once a day at midnight.  You can adjust the sync by manipulating the crontab in ./docker/simplefin/etc/crontab 

## Other resources
It is highly recommended you familiarize yourself with the documentation of both ActualBudget and Actual-SimpleFin-Sync.  Documentation for both linked below for your convenience.
- [ActualBudget](https://github.com/actualbudget/actual)
- [Actual-SimpleFin-Sync](https://github.com/duplaja/actual-simplefin-sync)

# Installation
## Prerequisites
You need to have Docker and Docker Compose running on your machine.  Helping you with this is outside the scope of this document.

## Starting the services
Download this repository to a location of your choice.  Next start the docker services with
```shell
docker-compose pull && docker-compose up --build -d
```

## Configuring the SimpleFin sync
This is the part where you should refer to the - [Actual-SimpleFin-Sync](https://github.com/duplaja/actual-simplefin-sync) documentation.

The main differences will be that you will be accessing the app through docker.
- **Setup** - Required after service startup to link the sync with your SimpleFin instance.
    ```shell
    docker exec -it actualbudget_simplefin node app.js --setup
    ```
- **Link** - Add or change account links
    ```shell
    docker exec -it actualbudget_simplefin node app.js --link
    ```
- **Sync** - Run a sync.  You shouldn't need to run this in normal operations as this will be done by the daily cron, but it can be useful for making sure things are working correctly without waiting for the cron.
    ```shell
    docker exec -it actualbudget_simplefin node app.js
    ```

