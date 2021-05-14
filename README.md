# Collection of my docker configurations

## Table of contents
* Install Docker
* Install docker-compose
* Portainer

## Install Docker
Installing Docker on the Raspberry Pi is quite simple. A single command on the terminal is all you need:

```bash
curl -sSL https://get.docker.com | sh
```

Alternative:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

Run the install script:

```bash
sh get-docker.sh
```

If you wish to run docker without running the command with `sudo` then you can add the default Raspberry Pi user `pi` to the `docker` group:

```bash
sudo usermod -aG docker $(whoami)
```

You will need to log out and back in or reboot your Raspberry Pi in order for the group change to occur.

## Install docker-compose

```bash
sudo apt-get -y install libffi-dev libssl-dev python3-dev python3 python3-pip
```

```bash
sudo pip3 install docker-compose # needs sudo to put it into path correctly
```