# Arch Linux setup and configuration

## Initial setup

After [bootstrapping](/bootstrap) run the `main.yml` playbook with manual
overrides for the new host, e.g.:

```shell
ansible-playbook -D -i hosts.yml main.yml --limit=gpd.wg.jaantoots.org -e ansible_host=gpd.tll.jaantoots.org -e ansible_user=root
```
