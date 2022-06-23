
# Install Nomad
- [Install Nomad](https://www.nomadproject.io/docs/install)
- [Nomad Deployment Guide](https://learn.hashicorp.com/tutorials/nomad/production-deployment-guide-vm-with-consul#start-nomad)
- [Keywords - datacenter, data_dir etc.](https://www.nomadproject.io/docs/configuration)
- Agent is a server that runs on every machine. You can run agent in server mode or client mode. Server agent is the brain of the cluster [read more...](https://circleci.com/docs/2.0/nomad/)

# Commands
## 1. Server
### `server.conf`
```
datacenter = "dc1"
data_dir = "/opt/nomad"

server {
  enabled = true
  bootstrap_expect = 1
}
```
Run agent with conf
```
sudo nomad agent -config=server.conf
```
## 2. Job
### _`job.nomad`_
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
See status
```
nomad status <ID>
```
## 3. Client
### `clinet.conf`
```
datacenter = "dc1"
data_dir = "/opt/nomad"

client {
  enabled = true
  servers = ["10.182.0.28:4647"] # ip of server
}
```
Run client
```
sudo nomad agent -config=client.conf
```
