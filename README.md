Barnacle
---------

This is a PoC of a remote shell using the Docker Remote API. This API
supports TLS Auth, so connections are encrypted.

What it does
------------

Provides a remote root shell to a Docker host. It does this by creating a
Docker container running on the host, but this container is explicitly
"uncontained" and may do most of the things a user might do via SSH.

Barnacle wraps around the docker cli and intercepts the 'host' argument.
All other arguments are passed to 'docker'. This is to demonstrate barnacle
as a possible addition to Docker itself.

How to use it
-------------

$ barnacle host [cmd] [args...]

This will connect to the host running Docker and execute the given command
and args. If no cmd is specified, it will default to '/bin/sh'.

What doesn't it do?
-------------------

Barnacle should be able to support rsh-like connections in order to use
RSH-compatible applications such as git and rsync. This does not
currently work, but I see no reason that it shouldn't be easy to
add.

Security
---------
Most Docker hosts do not expose the Docker Remote API on a TCP / TLS
endpoint. Some do, such as boot2docker. Docker does support TLS Auth,
but encrypted keys are not yet supported.

Barnacle might be useful in environments where the Remote API is
already exposed, but I would not yet advocate enabling a public
Remote API endpoint for the express purpose of using Barnacle.

It's very possible these recommendations will change as Docker and
Barnacle (or similar concepts) evolve.

Author(s)
----------
Eric Windisch (Docker, Inc)

---------------------------------------------------------------------
Copyright 2014  Docker, Inc. Distributed under the Apache 2 license.
