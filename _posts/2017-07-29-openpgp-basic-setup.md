---
layout: posts
comments: true
published: false
title: OpenPGP basic setup
categories:
  - security
tags:
  - openpgp
---

## Disclaimer

 * Tested on debian 9 "_Stretch_".

## Generate entropy

Install the `rng-tools` packet.

```sh
apt-get install rng-tools
```

Edit the file `/etc/default/rng-tools` and add this line:

```
HRNGDEVICE=/dev/urandom
```

Restart the service:

```sh
service rng-tools restart
```

## References

1. [Linux magazine #168 (fr)][1]

[1]: http://connect.ed-diamond.com/GNU-Linux-Magazine/GLMF-168