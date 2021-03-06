## evil-minions

![Evil Minions from the movie Despicable Me 2](https://vignette3.wikia.nocookie.net/despicableme/images/5/52/Screenshot_2016-02-10-01-09-16.jpg/revision/latest?cb=20161028002525)

`evil-minions` is a load generator for [Salt Open](https://saltstack.com/salt-open-source/). It is being developed at SUSE to aid [SUSE Manager](https://www.suse.com/products/suse-manager/) scalability testing.

### Status

Ongoing development, minimal functionality is there.

### Installation

 - install salt-minion 2015.8.12
 - clone this git repository

### Ideas and Usage

This project contains a script, `dumping-salt-minion`, that runs `salt-minion` while dumping all ZeroMQ traffic into a `/tmp/minion-dump.yml` file.

```
./dumping-salt-minion
# will create /tmp/minion-dump.yml
```

This "dump" can be fed to the `evil-minions` script, which will mimic the original minion by sending the same responses to equivalent requests coming from the master. It will by default simulate 10 copies of the original minions, the count can be changed via a commandline switch:

```
./evil-minions --count 5 <MASTER_FQDN>
```

### Known limitations
 - only the ZeroMQ transport is supported
 - `mine` events are not really reproduced
 - delays between responses are not reproduced
 - `state.sls`'s `concurrent` option does not really work
 - only `*` and exact minion id targeting are supported at the moment
