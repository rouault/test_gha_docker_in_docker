ARG BASE_IMAGE=ubuntu:20.04

FROM $BASE_IMAGE as builder

RUN apt-get update -y
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --fix-missing --no-install-recommends \
    docker.io
RUN service docker start
RUN docker pull mcr.microsoft.com/mssql/server:2017-latest
RUN docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=DummyPassw0rd'  -p 1433:1433 --name sql1 -d mcr.microsoft.com/mssql/server:2017-latest
RUN sleep 10
RUN docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -l 30 -S localhost -U SA -P DummyPassw0rd -Q "CREATE DATABASE TestDB;"

