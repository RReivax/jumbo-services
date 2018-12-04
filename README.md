# jumbo-services

To test, generate `inventory` directory with Jumbo then:
```
ln -s ~/.jumbo/[cluster]/playbooks/inventory inventory
ansible-playbook -i inventory blueprint.yml
```

Still requires to complete `inventory/groupvars/all` manually for Jinja2

# Inventory requirements

Jumbo's role is to generate the inventory folder with all necessary variables.

Example for a 3 nodes cluster with nodes `edge`, `master01`, `worker01` :
```
├── group_vars
│   └── all
├── hosts
└── host_vars
    ├── edge
    ├── master01
    └── worker01
```

All information relative to hosts should be placed in `host_vars` folder. For example, to generate the `master01_group` hostgroup we look at the `components` variable stored in `host_vars/master01`:
```
---
components:
- NAMENODE
- SECONDARY_NAMENODE
- RESOURCEMANAGER
- HDFS_CLIENT
- YARN_CLIENT
- ...
```

All information relative to services and the cluster in general should be stored in `group_vars/all`. For example to generate the blueprint for YARN and HDFS we should have:
```
---
HDFS:
  namenodes_FQDN:
  - master01.domain.local
  snamenode_FQDN: master01.domain.local
YARN:
  resourcemanagers_FQDN:
  - master01.domain.local
  container_max_memory: 1536
  nodemanager_resource_memory: 3072
  timeline_service_FQDN: edge.domain.local
```