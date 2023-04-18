How to set up Nginx reverse proxy.
-

#### What are ports?
- Ports are a way to identify specific processes or 
services on a computer that are communicating over a 
network. They are used to differentiate between different types of network 
traffic and ensure that data is sent to the correct destination.

#### What is a reverse proxy? How is it different to a proxy?
- A reverse proxy is a type of proxy server 
that sits between client devices and web 
servers. It acts as an intermediary, forwarding 
requests from clients to servers and returning 
the servers' responses to the clients. Unlike a 
traditional proxy, which forwards requests to a 
single server, a reverse proxy can distribute requests across multiple 
servers to improve performance and reliability.

![reverse_proxy.png](files%2Freverse_proxy.png)

##### What is Nginx's default configuration?
- Nginx's default configuration can be found in the "sites-available" 
directory. This directory typically contains a default configuration 
file that specifies how Nginx should handle incoming requests, including 
which ports to listen on, which server blocks to use, and which 
backend servers to connect to.

#### How do you set up a Nginx reverse proxy?

1. First we need to use `vagrant up` in our VS Code terminal.
2. Next step it to use `vagrant ssh` in GitBash terminal (in our virtualisation folder).
3. Make sure that Nginx is installed: `sudo apt-get install nginx` or `sudo systemctl status nginx`.
4. Now we need to navigate to Nginx configuration file : `cd /etc/nginx/sites-available/`.
5. Create reverse proxy file in the folder: `sudo nano reverse-proxy`.
6. In that file type :

```
server {
   listen 80;
   server_name 192.168.10.100;

   location / {
       proxy_pass http://192.168.10.100:3000;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       proxy_set_header X-Forwarded-Proto $scheme;
   }
}
```
7. Next go back to main directory: `cd` & navigate to: `cd /etc/`.
8. Use `sudo nano hosts` & at the end of the file add:

```
192.168.1.100   backend-server
```
9. Create a symbolic link to the new configuration 
file in the "/etc/nginx/sites-enabled" directory by running the command 
`sudo ln -s /etc/nginx/sites-available/reverse-proxy /etc/nginx/sites-enabled/`.
10. Check configuration file for errors by using: `sudo nginx -t`.
11. Reload Nginx : `sudo systemctl reload nginx`.
12. Now we can access our "Sparta App" by typing IP in browser.

