
# Install Nomad
---
- [Install Nomad](https://www.nomadproject.io/docs/install)
- [Nomad Deployment Guide](https://learn.hashicorp.com/tutorials/nomad/production-deployment-guide-vm-with-consul#start-nomad)

# Commands
---
## **1. Server**
### Run server
```
sudo nomad agent -config=server.conf
```
### _server.conf_
```
datacenter = "dc1"
data_dir = "/opt/nomad"

server {
  enabled = true
  bootstrap_expect = 1
}
```

## **2. Job**
---
### _job.nomad_
```
job "web" {
    datacenters = ["dc1"]
    group "api" {
       task "webserver" {
         driver = "exec"
         config {
             command = "./binary"
         }
       }
    }
}
```
Run job
```
nomad job run job.nomad
```
Remove job
```
nomad job stop -purge <ID>
```

## **3. Client**
---
### Run clinet
```
sudo nomad agent -config=server.conf
```
### _clinet.conf_
```
datacenter = "dc1"
data_dir = "/opt/nomad"

client {
  enabled = true
  servers = ["10.182.0.28:4647"] # ip of server
}
```
