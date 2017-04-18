# Replication module is designed for DBaaS.
## This play book has been triggered on Ansible Tower 3.0

### POSTMAN POST CALL TO TRIGGER 

```

https://ansibletower.dbaas.com/api/v1/job_templates/$NUMBER/launch/

{
"extra_vars" :
{
  "api": {
    "master": "192.168.1.1",
    "slave": "192.168.1.2",
  }
}

```

# NOTE:

* Tag Inventory against Slave to make changes to my.cnf file
* This job will trigger the playbooks/dbaas_replication.yml and inturn calls the roles. 
* It can configure only two servers. Master and Slave . Also it can configure Slave1 as master to another Slave2, mention Slave1 ip under master argument keep the label as it is and Slave2 ip under slave label. 
