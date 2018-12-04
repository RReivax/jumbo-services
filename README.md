# jumbo-services

To test, generate `inventory` directory with Jumbo then:
```
ln -s ~/.jumbo/[cluster]/playbooks/inventory inventory
ansible-playbook -i inventory blueprint.yml
```

Still requires to complete `inventory/groupvars/all` manually for Jinja2