# icon-analytics-airflow-docker

Docker deployment of airflow customized for use with [icon-etl-airflow](https://github.com/insight-icon/icon-etl-airflow), a set of dags to analyze the ICON Blockchain.

### Usage

To run the basic stack which includes:
- Airflow webserver, scheduler, and worker
- Postgres, redis, and flower, 
- Nginx

1. Install docker and docker-compose.  
2. To pull in dags, you have two options, creating a local dags folder with the DAGs or using git-sync and configuring the remote repo.  Both options are viable but it is recommended to store the dags in it's own repository, ie 

```bash
git clone https://github.com/insight-icon/icon-etl-airflow dags
```

3. You will need an S3 bucket and credentials to to read and write to that bucket.  If using ec2, it is advised to use an instance profile with appropriate permissions or you can use API keys and populate them in the .env file. 

4. At the root of this repo, run: 
```bash
docker-compose up -d 
``` 

Navigate to `localhost` in your browser and you should find airflow running after about 30 seconds. 

5. Modify the `variables.json` file with appropriate values. Then, inside the airflow console, go to `Admin` -> `Variables` and load the variables.json file with the `Choose File` option.


To run with more advanced / indevelopment options, modify the `docker-compose.*.override.yml` or include it in the `docker-compose` call. 

There are two alternate configuration. 

1. Prometheus addons 
- Will monitor your nodes health and metrics from the airflow execution 
2. Worker 
- For running a multi-worker distributed environment

Both these options are for advanced users only. 

### Development 

This repo is meant for local development of dags.  To run this in production, please see [terragrunt-icon-analytics](https://github.com/insight-icon/terragrunt-icon-analytics). When writing new dags, it is important remember to restart the scheduler sometimes to pick up the changes made to the dag.  Using this repo and working locally is very helpful when building dags. 
