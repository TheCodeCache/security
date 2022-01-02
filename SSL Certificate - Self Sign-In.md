# Self-Signed X.509 Certificate — 

install openssl as follows:  
```shell
ubuntu@ip-172-31-42-44:~/flask$ sudo apt-get install openssl
```
The above command is run on an AWS EC2 ubuntu machine from this directory: /home/ubuntu/flask  

To generate a `self-signed` ssl certificate and key, just run below cmd -  

```shell
ubuntu@ip-172-31-42-44:~/flask$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-self-signed.key -out /etc/ssl/certs/nginx-self-signed.crt
```

and the openssl continues to ask queries like below after running the above cmd.  

```shell
ubuntu@ip-172-31-42-44:~/flask$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-self-signed.key -out /etc/ssl/certs/nginx-self-signed.crt
Generating a RSA private key
.......................................................................................+++++
........................................+++++
writing new private key to '/etc/ssl/private/nginx-self-signed.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:Maharashtra
Locality Name (eg, city) []:Mumbai Bombay
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:equity-updates.com, www.equity-updates.com, 13.232.222.62
Email Address []:softmanoranjan@gmail.com
ubuntu@ip-172-31-42-44:~/flask$ 
```

The above command will generate a pair of files, a certificate file and another a key file  

and, both of these files could be found at this location on the ubuntu machine:  
/etc/ssl/private/nginx-self-signed.key  
/etc/ssl/certs/nginx-self-signed.crt  

To use the above self-signed certificate and key files is as follows:  

```shell
ubuntu@ip-172-31-42-44:~/flask$ sudo vi /etc/nginx/sites-enabled/myflaskapp
```
In the above `/etc/nginx/sites-enabled/` is the nginx directory.  and `myflaskapp` is a config file with random name.  

```shell
# existing content in this config file: /etc/nginx/sites-enabled/myflaskapp
server {
    listen 80;
    server_name equity-updates.com www.equity-updates.com 13.232.222.62;

    access_log  /var/log/nginx/myapp.log;

    location / {
        proxy_pass http://127.0.0.1:8000;
    }
}
```

```shell
# updated content with ssl details in the above config file: /etc/nginx/sites-enabled/myflaskapp 
server {
    listen 80;
    listen 443 ssl;
    server_name equity-updates.com www.equity-updates.com 13.232.222.62;

    ssl_certificate /etc/ssl/certs/nginx-self-signed.crt;
    ssl_certificate_key /etc/ssl/private/nginx-self-signed.key;

    access_log  /var/log/nginx/myapp.log;

    location / {
        proxy_pass http://127.0.0.1:8000;
    }
}
```

and now, test the above updated nginx config file as follows to ensure for correct syntax:  

```shell
ubuntu@ip-172-31-42-44:~/flask$ sudo nginx -t
```
if things go well, then it'll return like below, else we need to fix issues with above config file.  

```shell
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

we do not need to restart nginx server, rather we can just reload the config like below, and it's done  

```shell
ubuntu@ip-172-31-42-44:~/flask$ sudo nginx -s reload
```

and then hit the url https://equity-updates.com in browser, we'd get something like this:  

![image](https://user-images.githubusercontent.com/26399543/147892238-1d08574f-e421-4370-86dd-02647afe95c9.png)  

and, once we click on continue like down below in the above image, it'll show us the correct response from web server.  

![image](https://user-images.githubusercontent.com/26399543/147892259-0c77cd45-6db8-4af1-b8ef-b87548e48cb2.png)  


**Recommendations —**  

Using self-signed certificates is not recommended and presents a potential security risk.  
For production systems, use a trusted certification authority (CA) to issue certificates.

