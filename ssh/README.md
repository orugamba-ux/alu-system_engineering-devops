# SSH

Scripts for connecting to my server with ssh.

- `0-use_a_private_key` - connects to the server with the key in `~/.ssh/school`

Run it like this:

```
$ ./0-use_a_private_key
ubuntu@6993-web-01:~$
```

The key has to be in `~/.ssh/school` on your own machine first, and the
permissions need to be tight or ssh will refuse to use it:

```
$ chmod 600 ~/.ssh/school
```
