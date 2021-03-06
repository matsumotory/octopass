octopass
========

Management linux user and authentication by therganization/team on Github.

[![Travis](https://img.shields.io/travis/linyows/octopass.svg?style=flat-square)][travis]
[![GitHub release](http://img.shields.io/github/release/linyows/octopass.svg?style=flat-square)][release]
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)][license]
[![Go Documentation](http://img.shields.io/badge/go-documentation-blue.svg?style=flat-square)][godocs]

[travis]: https://travis-ci.org/linyows/octopass
[release]: https://github.com/linyows/octopass/releases
[license]: https://github.com/linyows/octopass/blob/master/LICENSE
[godocs]: http://godoc.org/github.com/linyows/octopass

Description
-----------

This is linux user management tool by the organization/team on github, and authentication.
Depending on github for user management, there are certain risks,
but features easy handling and ease of operation.

Usage
-----

### NSS command

This is output in the same display as file such as passwd, shadow and group.
For detail `--help`.

```sh
$ nss-octopass passwd
chun-li:x:14301:2000:managed by nss-octopass:/home/chun-li:/bin/bash
dhalsim:x:8875:2000:managed by nss-octopass:/home/dhalsim:/bin/bash
ken:x:5458:2000:managed by nss-octopass:/home/ken:/bin/bash
ryu:x:74049:2000:managed by nss-octopass:/home/ryu:/bin/bash
sagat:x:93011:2000:managed by nss-octopass:/home/sagat:/bin/bash
zangief:x:8305:2000:managed by nss-octopass:/home/zangief:/bin/bash
```

### Keys command

Get public keys for AuthorizedKeysCommand in sshd(8)

```sh
$ octopass -t <token> keys <user@github>
```

#### SSHD Configuration

```
AuthorizedKeysCommand /usr/bin/octopass --config=/etc/octopass.conf keys %u
AuthorizedKeysCommandUser root
UsePAM yes
PasswordAuthentication no
```

### Pam Command

Authenticate with github for pam_exec(8)

```sh
$ echo <token@github> | env PAM_USER=<user@github> octopass -t <token> pam
```

#### PAM Configuration

```
#@include common-auth
auth requisite pam_exec.so quiet expose_authtok log=/var/log/octopass.log /usr/bin/octopass --config=/etc/octopass.conf pam
auth optional pam_unix.so not_set_pass use_first_pass nodelay
```

Install
-------

To install, use `go get`:

```bash
$ go get -d github.com/linyows/octopass
```

Contribution
------------

1. Fork ([https://github.com/linyows/octopass/fork](https://github.com/linyows/octopass/fork))
1. Create a feature branch
1. Commit your changes
1. Rebase your local changes against the master branch
1. Run test suite with the `go test ./...` command and confirm that it passes
1. Run `gofmt -s`
1. Create a new Pull Request

Author
------

[linyows](https://github.com/linyows)
