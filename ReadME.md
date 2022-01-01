# Deploy with Docker ReportPortal
ReportPortal can be easily deployed using Docker-Compose.

## Install Docker
    Docker is supported by all major Linux distributions, MacOS and Windows

    Download and install Docker, Docker Compose

## Note:

    If you use Docker for Windows or MacOS, make sure there is at least 3gb dedicated for Docker. For Windows native docker:
    Image

    Note: for Windows users. *Docker for Windows requires 64-bit Windows 10 Pro and Microsoft Hyper-V.

## Deploy ReportPortal with Docker
### 1) Make sure the Docker Engine and Compose are installed.

### 2) Download the latest ReportPortal Docker compose file from here. You can make it by run the following command:

    curl -LO https://raw.githubusercontent.com/reportportal/reportportal/master/docker-compose.yml

### 3) Make the ElasticSearch configuration prerequisites for the analyzer service

    a) Set {vm.max_map_count} kernel setting before ReportPortal deploying with the following Commands

    b) Give right permissions to ElasticSearch data folder using the following commands:

    mkdir -p data/elasticsearch
    chmod 777 data/elasticsearch
    chgrp 1000 data/elasticsearch
    For more details about ElasticSearch visit ElasticSearch guide

### 4) > OPTIONAL

    PostgreSQL Performance Tuning

    Depends on your hardware configuration and parameters of your system, you can additionally optimize your PostgreSQL performance by adding the following parameters to "command" option in the Docker compose file:

    -c effective_io_concurrency=
    -c shared_buffers=
    -c max_connections=
    -c effective_cache_size=
    -c maintenance_work_mem=
    -c random_page_cost=
    -c seq_page_cost= 
    -c min_wal_size= 
    -c max_wal_size=
    -c max_worker_processes=
    -c max_parallel_workers_per_gather=
    Please choose set the values of these variables that are right for your system.

    You can also change PostgreSQL host by passing a new value to POSTGRES_SERVER environment variable.

### 5) Start the application using the following command:

    docker-compose -p reportportal up -d --force-recreate
    Where:

    -p reportportal adds project prefix 'reportportal' to all containers
    up creates and starts containers
    -d daemon mode
    --force-recreate Re-creates containers if there any
    Useful commands:

    docker-compose logs shows logs from all containers
    docker logs <container_name> shows logs from selected container
    docker ps -a | grep "reportportal_" | awk '{print $1}' | xargs docker rm -f Deletes all ReportPortal containers

### 6) Open your web-browser with an IP address of the deployed environment at port 8080

    You can get the host IP address by using the following docker commands:

    If you run Docker on macOS or Windows with Docker for Mac, Docker for Windows

    docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' CONTAINER_ID_OR_NAME
    If you run Docker on Linux, you can find your public IP address in Linux Terminal

    curl ifconfig.co
    ReportPortal address:

    http://IP_ADDRESS:8080
    Use the following login\pass to access:

    Default User: default\1q2w3e
    Administrator: superadmin\erebus
    Please change the admin password for better security