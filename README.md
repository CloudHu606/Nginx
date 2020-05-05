# Nginx
_Nginx is a web server which can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache_

_systemd is a new init system and system manager_ / _sysvinit is a traditional SysVinit manager_

### install 
$ sudo yum install epel-release && yum install nginx   [On CentOS/RHEL]

$ sudo dnf install nginx                               [On Debian/Ubuntu]

$ sudo apt install nginx                               [On Fedora]

### check verison
$ nginx -v

$ nginx -V    // show more details 

### check nginx configuration 
$ sudo nginx -t

$ sudo nginx -T    // show more details 

### start nginx service 
$ sudo systemctl start nginx #systemd

$ sudo service nginx start   #sysvinit

### enable nginx service (it auto-start at boot time)
$ sudo systemctl enable nginx #systemd

$ sudo service nginx enable   #sysvinit

### restart nginx service 
$ sudo systemctl restart nginx #systemd

$ sudo service nginx restart   #sysvinit

### reload nginx service 
$ sudo systemctl reload nginx #systemd

$ sudo service nginx reload   #sysvinit

### view nginx status 
$ sudo systemctl status nginx #systemd

$ sudo service nginx status   #sysvinit

### stop nginx service 
$ sudo systemctl stop nginx #systemd

$ sudo service nginx stop   #sysvinit

### nginx command help
$ systemctl -h nginx

###### default.conf example: 
```
server {
    listen       80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }  
}
```
###### webName.conf example:
```
server {
    listen 80;
    listen 443 ssl;
    ssl on;
    ssl_ciphers 'xxx';
    ssl_certificate     /path/www.example.com.chained.crt;
    ssl_certificate_key /path/www.example.com.key;

    server_name www.website.com;
    root app-path;

    # force https-redirects
    if ($scheme = http) {
        return 301 https://$server_name$request_uri;
    }
    
    location ~ xxx {
	     return 301 https://$server_name/xyz;
    }                  
	
	location / {
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
        proxy_read_timeout 5m;
        proxy_connect_timeout 5m;
        proxy_redirect off;
        proxy_pass http://localhost:port#;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

}

```
[full ngnix config exmaple](https://www.nginx.com/resources/wiki/start/topics/examples/full/#proxy-conf)


### Renew SSL Certification in Nginx Server 

path: /etc/nginx/conf.d/certs/

Put SSL provider files to certs folder 

