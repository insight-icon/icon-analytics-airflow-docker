# icon-analytics-airflow-docker

Docker deployment of airflow customized for use with [icon-etl-airflow](https://github.com/insight-icon/icon-etl-airflow), a set of dags to analyze the ICON Blockchain.

### Usage

To run the basic stack which includes:
- Airflow webserver, scheduler, and worker
- Postgres, redis, and flower, 
- Nginx

1. Install docker and docker-compose.  
2. At the root of this repo, clone or fork [icon-etl-airflow](https://github.com/insight-icon/icon-etl-airflow) and rename the directory `dags`. 
```bash
git clone https://github.com/insight-icon/icon-etl-airflow dags
```
3. At the root of this repo, run: 
```bash
docker-compose up -d 
``` 

Navigate to `localhost` in your browser and you should find airflow running after about 30 seconds. 

To run with more advanced / indevelopment options, modify the `docker-compose.*.override.yml` or include it in the `docker-compose` call. 

There are two alternate configuration. 

1. Prometheus addons 
- Will monitor your nodes health and metrics from the airflow execution 
2. Worker 
- For running a multi-worker distributed environment

Both these options are for advanced users only. 

### Development 

This repo is meant for local development of dags.  To run this in production, please see [terragrunt-icon-analytics](https://github.com/insight-icon/terragrunt-icon-analytics). When writing new dags, it is important remember to restart the scheduler sometimes to pick up the changes made to the dag.  Using this repo and working locally is very helpful when building dags. 
