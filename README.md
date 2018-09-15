# Test HTTP Load Balancing with NGINX

On the back end web servers, run the following commands to install NGINX:

```
$ sudo apt-get install -y nginx
$ uname -n | sudo tee /var/www/html/index.html
```

On the load balancer, run the follow commands:

```
$ sudo apt-get install -y nginx
```

Use the following as the contents of /etc/nginx/sites-available/default:

```
upstream web_backend {
  # Uncomment for the IP Hashing load balancing method:
  # ip_hash;

  # Uncomment for the Least Connected load balancing method:
  # least_conn;

  # Replace the IP addresses with the IP addresses
  # (or host names) of your back end web servers.
  # Examples:
  # server www1.example.com:8080;
  # server 192.168.1.100;

  server 10.11.12.51;
  server 10.11.12.52;
}

server {
  listen 80;
  location / {
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://web_backend;
  }
}
```

Make NGINX read the new configuration by running the following commands

Check the configuration syntax

```
$ sudo nginx -t
```
The output must look like :
```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Reload the configuration

```
$ sudo service nginx reload
```

Continuously send a Get request to the load balancer address with the command (2 seconds interval between calls)

```
$ watch -n 2 curl http://10.11.12.50:80
```

The output must show alternatively web01, web02, and so on :

```
Every 2,0s: curl http://10.11.12.50:80
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                               Dload  Upload   Total   Spent    Left  Speed
 0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0 100     6  100     6    0     0      6      0  0:00:01 --:--:--  0:00:01  2000
web01
web02
web01
web02
web01
web02
...
```
---

Resources

* [Vagrant](https://www.vagrantup.com/)
* [Nginx http load_balancing documentation](http://nginx.org/en/docs/http/load_balancing.html)
* [load-balancing-with-nginx-cheat-sheet.pdf](./load-balancing-with-nginx-cheat-sheet.pdf)
