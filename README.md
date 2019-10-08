# Arch Linux setup and configuration

## Initial setup

After [bootstrapping](https://github.com/jaantoots/arch-bootstrap) run the
`main.yml` playbook with necessary manual overrides for the new host, e.g.:

```shell
ansible-playbook -D -i hosts.yml main.yml --limit=gpd.wg.jaantoots.org -e ansible_host=gpd.tll.jaantoots.org -e ansible_user=root
```

## TODO

Missing configuration:

- firewall (nftables)

Manual tasks:

- `base16_default-dark` command run
- i3line compilation
- xorg and lock screen backgrounds
- add SSH key to cloud.jaantoots.org
- password store repository clone
- add SSH key to Github
- clone `.private`
- obtain GPG keys

Maybe personal user configuration should not be in the scope of this
repository?

## Notes

Extract space separated lists of packages installed by different tasks:

```shell
sed -nE '
    /pacman:/{
        n;h;x;s/.*//;x;
        :a;n;/^$/bb;/- /!d;H;$bb;ba
    };h;d;
    :b;x;s/^\n//;s/ +- (\w+)/\1/g;s/\n/ /g;p;d
    ' roles/*/tasks/main.yml
```

And get installed sizes of installed package trees for each group:

```shell
sed -nE '
    /pacman:/{
        n;h;x;s/.*//;x;
        :a;n;/^$/bb;/- /!d;H;$bb;ba
    };h;d;
    :b;x;s/^\n//;s/ +- (\w+)/\1/g;s/\n/ /g;s/.*/pactree -su \0/e;s/\n/ /g;s/.*/expac -S %m \0/e;s/\n/+/g;p;d
    ' roles/*/tasks/main.yml | bc | numfmt --to=iec
```
