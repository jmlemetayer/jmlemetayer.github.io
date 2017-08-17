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

## Generate the master key

```sh
gpg --full-gen-key
```
And use the following configuration:

 * Key kind: `(4) RSA (sign only)`
 * Key size: `4096`
 * Key expiration: `0 = key does not expire`

Then you can enter your real name and email address.

## References

1. [Linux magazine #168 (fr)][1]

[1]: http://connect.ed-diamond.com/GNU-Linux-Magazine/GLMF-168
