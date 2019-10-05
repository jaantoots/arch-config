# Arch Linux setup and configuration

## Initial setup

After [bootstrapping](/bootstrap) run the `init.yml` playbook with a manually
specified host:

```shell
ansible-playbook -D -i gpd.tll.jaantoots.org, init.yml 
```
