haproxsy-lab
-------------

Idea: setup several http servers and put haproxy in front to load balance!

 - one httpd with many virtualservers
 - one haproxy in front pointing to these

usage
----------

Copy example inventory file:
```bash
cp inventory-example inventory
```

Change the the IP address of the lab machine:
```bash
$EDITOR inventory
```
Run ansible:
```bash
ansible-playbook -i inventory site.yml
```

At this point you'll have an haproxy on IP of the lab machine port 80 with some backend servers pointing to the virtualservers. Try it out by sshing into the lab machine and run:

```bash
[cloud-user@lab ~]$ curl frontend.example.com
<html>
<title> frontend.example.com </title>

gethostname: lab </br>
server_name: frontend.example.com </br>
http_host: frontend.example.com </br>
path: /var/www/vhosts/3 </br>

</html>
[cloud-user@lab ~]$ curl frontend.example.com
<html>
<title> frontend.example.com </title>

gethostname: lab </br>
server_name: frontend.example.com </br>
http_host: frontend.example.com </br>
path: /var/www/vhosts/1 </br>

</html>
[cloud-user@lab ~]$ curl frontend.example.com
<html>
<title> frontend.example.com </title>

gethostname: lab </br>
server_name: frontend.example.com </br>
http_host: frontend.example.com </br>
path: /var/www/vhosts/2 </br>

</html>
[cloud-user@lab ~]$ curl frontend.example.com
<html>
<title> frontend.example.com </title>

gethostname: lab </br>
server_name: frontend.example.com </br>
http_host: frontend.example.com </br>
path: /var/www/vhosts/3 </br>

</html>
[cloud-user@lab ~]$
```


