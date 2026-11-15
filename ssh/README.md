# SSH

Scripts and config for making an ssh key and connecting to my server with it.

- `0-use_a_private_key` - connects to the server with the key in `~/.ssh/school`
- `1-create_ssh_key_pair` - makes a 4096 bit rsa key pair called `school`
- `2-ssh_config` - client config so ssh uses that key and never asks for a
  password
- `100-puppet_ssh_config.pp` - the same two settings, but done with puppet
  instead of by hand

Make the key first, then move it where ssh looks for it:

```
$ ./1-create_ssh_key_pair
$ mv school school.pub ~/.ssh/
$ chmod 600 ~/.ssh/school
```

Copy the config into place as well:

```
$ cp 2-ssh_config ~/.ssh/config
```

Then connect:

```
$ ./0-use_a_private_key
ubuntu@6993-web-01:~$
```

You can check the config is being picked up with `ssh -G <server-ip>`, it
should print `identityfile ~/.ssh/school` and `passwordauthentication no`.

The school public key is also in `~/.ssh/authorized_keys` on the server so the
graders can log in as `ubuntu` too.

Puppet can set the same two lines in `/etc/ssh/ssh_config` for you:

```
$ sudo puppet apply 100-puppet_ssh_config.pp
```
