# named-resolver

This is an ISC `bind` (named) DNS resolver with DNSSEC validation that mirrors the `ROOT` zone.
Mirroring the ROOT zone improves performance and reduces load on the ROOT servers.

It runs in a `chroot` which is a little unnecessary, but its not hard, so why not.

The default is to allow **ANYBODY** to send queries to this server. If it is on a
public IP, without an appropriate firewall, this means it **WILL** be D/DoS'ed - so
don't do that.

If its going to be on a public IP Address, change this line first

	acl allowed-nets { any; };

so instead of `any` you have a semi-colon separated list of the IPs / subnets you want permission
to query this server.


## IPv6 ##

NOTE: this is currently configured to only support IPv4. This is becuase `bind` is really laggy if
it is configured for IPv6, but IPv6 connectivity is not available.

To re-enabled IPv6, remove the `-4` in the `inittab` file, and change the line

	listen-on-v6 { none; };

to

	listen-on-v6 { any; };
