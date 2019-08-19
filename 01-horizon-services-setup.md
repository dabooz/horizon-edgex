# Horizon Dev Services Setup

This document will give you the steps needed to get a small dev instance of the services running. 
It will not, and should not, be used to serve edge devices in a production environment. 
However, it is sufficient to test services.

## Pre-requisites

+ OS: Ubuntu server, latest build recommended.  Instructions assume this.
+ VM: 1Gb RAM, 20Gb storage, 1vCPU, root access

## Initial setup

Update utilities.  *NOTE*: You will perform all of these tasks as root through `sudo`.

```
sudo -s
apt-get -y update
apt-get install -y jq make gcc
```

Install Go from source (don't use `apt` or `snap`) since the `src` and `pkg` and `bin` folders will be needed.

```
curl https://dl.google.com/go/go1.11.4.linux-amd64.tar.gz | tar -xzf- -C /usr/local/
export PATH=$PATH:/usr/local/go/bin
```

Install Docker from source (to get the required newest version), and utilities.

```
curl -fsSL get.docker.com | sh
apt-get install -y docker-compose
```

Set up your GOPATH and related environment variables.  *NOTE*: The GOPATH _must_ be under $(USER) or the test scripts will throw errors.

```
mkdir -p /go/src/github.com/open-horizon
export GOPATH=/go
export ANAX_SOURCE=/go/src/github.com/open-horizon/anax
```

Install required `go` utilities.  *NOTE*: You must use this method, and not `apt`, or the test scripts will throw errors.

```
go get -u github.com/kardianos/govendor
```

Clone the Open Horizon project code.

```
cd /go/src/github.com/open-horizon
git clone https://github.com/open-horizon/anax.git
```

## Next

[Build and Run](02-build-and-run-horizon.md) the Horizon Dev Services.