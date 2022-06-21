# fritzinfluxdb

https://github.com/karrot-dev/fritzinfluxdb

## Prepare the fritzinfluxdb working directory

To persist data and configuration of your fritzinfluxdb instance you need to create a directory on your Raspberry system that will be used by docker:

``` bash
mkdir -p $HOME/app
cd ~/app
git clone https://github.com/karrot-dev/fritzinfluxdb.git
cd fritzinfluxdb
docker build -t fritzinfluxdb .
```

## Start fritzinfluxdb via docker

``` bash
docker run -d -v $HOME/docker/fritzinfluxdb/config/fritzinfluxdb.ini:/app/fritzinfluxdb.ini --name fritzinfluxdb fritzinfluxdb
```

``` bash
docker run -d -v $HOME/docker/fritzinfluxdb/config/fritzinfluxdb-k3s.ini:/app/fritzinfluxdb.ini --name fritzinfluxdb-k3s fritzinfluxdb
```