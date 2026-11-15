# Web Server

Scripts for setting up nginx on my server and pointing my domain at it.

- `0-transfer_file` - scp a file to the server using the school key
- `1-install_nginx_web_server` - installs nginx and serves "Holberton School
  for the win!" on port 80
- `2-setup_a_domain_name` - the domain I pointed at the server, its A record
  goes to `18.171.164.6`
- `3-redirection` - adds a 301 from `/redirect_me` to a youtube video
- `4-not_found_page_404` - adds a custom 404 page that says "Ceci n'est pas
  une page"
- `5-design_a_beautiful_404_page.html` - a nicer looking 404 page

The scripts run on the server, not on my laptop:

```
$ ./0-transfer_file 4-not_found_page_404 18.171.164.6 ubuntu ~/.ssh/school
$ ssh -i ~/.ssh/school ubuntu@18.171.164.6
ubuntu@6993-web-01:~$ sudo ./4-not_found_page_404
```

Checking it worked:

```
$ curl -sI 18.171.164.6/redirect_me | head -1
HTTP/1.1 301 Moved Permanently
$ curl 18.171.164.6/xyz
Ceci n'est pas une page
```

Only run each script once. The `sed` lines add to
`/etc/nginx/sites-enabled/default` every time, so running one twice leaves two
copies of the same block and nginx refuses to start. `sudo nginx -t` tells you
which line is the duplicate before you restart anything.
