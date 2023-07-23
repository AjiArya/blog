---
title: "Resync Broken Juju Database (MongoDB)"
description: "How to resync Juju Database (MongoDB)"
date: "2023-07-23"
tags: ["Juju", "Canonical",  "Ubuntu", "MongoDB", "Troubleshooting"]
categories: ["Juju"]
ShowToc: true
TocOpen: true
---

# Environment
- Juju DB snap channel: 4.0/stable
- Juju controller agent: 2.9.0
- Operating System: Ubuntu 20.04 LTS
- Deployment: Juju HA

# Symptom
1. Juju controller does not bind port `37017` / MongoDB Port
2. Following error log can be found from `/var/snap/juju-db/common/logs/mongodb.log`
```bash
[replication-0] We are too stale to use <IP_ADDRESS>:37017 as a sync source. Blacklisting this sync source because our last fetched timestamp:
[replication-0] could not find member to sycn from
```

# Guide
## 1. Pausing Juju Controller and Juju Database (MongoDB)
Execute on all juju controller
1. Switch to controller model
```bash
juju switch controller
```

2. Login to juju controller
```bash
juju ssh <machine_id>
```

3. Stop all juju controller agent
Run following command inside 
```bash
sudo systemctl stop jujud-machine-<machine_id>.service
```

4. Gracefully stop Juju Database (MongoDB)
```bash
sudo snap stop juju-db
```

## 2. Backup Juju Database
Execute on troubled juju controller

Backup DB
```bash
sudo mv /var/snap/juju-db/common/db /var/snap/juju-db/common/db.orig
sudo mkdir /var/snap/juju-db/common/db
sudo chmod 700 /var/snap/juju-db/common/db
```

## 3. Start database
Execute on all juju controller
1. Start all Juju Database (MongoDB)
```bash
sudo snap start juju-db
```

2. Verify sync process
You should see the key `statStr` has value as `SECONDARY`
```bash
# Get user and password
export user=$(sudo grep tag /var/lib/juju/agents/machine-*/agent.conf | cut -d' ' -f2)
export password=$(sudo grep statepassword /var/lib/juju/agents/machine-*/agent.conf | cut -d' ' -f2)

# Make sure the troubled node already run as SECONDARY
mongo 127.0.0.1:37017/juju -u "${user}" -p "${password}" --sslAllowInvalidCertificates --ssl --authenticationDatabase admin --eval "printjson(rs.status())"
```

# Reference
- https://cloud.garr.it/support/kb/juju/Juju_ha_mongodb_recovery/
