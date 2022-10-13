# DBRepo - Airquality Data Stream
This folder contains a python script which periodically scrapes real time austrian airquality data (every 30 minutes) from [luft.umweltbundesamt.at](https://luft.umweltbundesamt.at/pub/map_chart/index.pl). This stream data is then directly persisted in a DBRepo instance via its build in Rabbit MQ broker.

# Installation
**_NOTE:_** Before proceeding to the installation, make sure that you provide your DBRepo login credentials in the `.env` file (for more, see next chapter _Configuartion_).

The whole application is dockerized and can be easily started using the provided Dockerfile:
```sh
docker build . -t airquality-stream        # create an image
docker run airquality-stream               # run a container
```
[Alternative]: The data stream script can also be started without Docker. Therefore it is important to have `python3` and `pip3` and all necessary libraries in `requirements.txt `:
```sh
apt install python3 python3-pip            # install python and pip manager
pip3 install -r requirements.txt           # install all necessary libraries
python3 airquality.py                      # run the airquality data stream
```
# Configuartion
All necessary configuations such as the DBRepo instance (default [https://dbrepo.ossdip.at](https://dbrepo.ossdip.at)) and credentials and database location to insert the stream data can be changed in the `.env` file. Please make sure that all enviorment variables are provided. 

**_NOTE:_** There is no need to create any DBRepo database or table, these are generated automatically with the provided information.
```sh
DBREPO_RABBITMQ_BROKER_URL=<DBRepo Rabbit MQ URL/IP> (default 128.130.202.19)
DBREPO_RABBITMQ_BROKER_PORT=<DBRepo Rabbit MQ Port> (default 5672)
DBREPO_HTTP_URL=<DBRepo instance> (default https://dbrepo.ossdip.at)

AIRQUALITY_DBREPO_USERNAME=<your DBRepo username>
AIRQULAITY_DBREPO_PASSWORD=<your DBRepo password>
AIRQULAITY_DBREPO_DB_NAME=<DBRepo Database name> (default AirQuality)
AIRQUALITY_DBREPO_DB_DESCRIPTION=<DBRepo Database description>
```
