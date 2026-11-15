# SSH

Scripts for making an ssh key and connecting to my server with it.

- `0-use_a_private_key` - connects to the server with the key in `~/.ssh/school`
- `1-create_ssh_key_pair` - makes a 4096 bit rsa key pair called `school`

Make the key first, then move it where ssh looks for it:

```
$ ./1-create_ssh_key_pair
$ mv school school.pub ~/.ssh/
$ chmod 600 ~/.ssh/school
```

Then connect:

```
$ ./0-use_a_private_key
ubuntu@6993-web-01:~$
```

The key is protected by a passphrase, so ssh asks for it when you connect.
