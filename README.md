# docker

<html><body>
  <section>
  <h3>Fundamentals of Virtualization</h3>
  <p>Vertualization is a process of creating multiple virtual machine on single set of existing hardware machine.</p> 
   <p>There are two widely used ways of virtualization: Virtual Machine and Conatainer.
  </section>  
  <section>
  <h3>Installation :</h3>
    <p>Edit</p>
  </section>
  <section>
    <h3> MySQL</h3>
    <h4>Downloading a MySQL Server Docker Image:</h4>  
    <p><code>$docker pull mysql/mysql-server:tag</code>  #tag[5.5, 5.6, 5.7, 8.0, or latest]</p>
    <p><code>$docker images</code></p>
    <pre>REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
mysql/mysql-server   latest              12a8d88596c0        4 days ago          294MB
hello-world          latest              fce289e99eb9        6 months ago        1.84kB
</pre>
    <h4>Start a new Docker container for the MySQL Server:</h4>
  <p><code>$docker run --name=mysql1 -d mysql/mysql-server:latest</code> #name is optional. If not provided will be assigned one. #-d  makes the container run in the background.<p>
    <p><code>docker run --name=mysql1  -e MYSQL_ROOT_HOST=% -p 3306:3306 -d mysql/mysql-server</code></p>
     <p><code>$docker ps</code></p><pre>CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS                   PORTS                 NAMES
10ed6e9fd73b        mysql/mysql-server:latest   "/entrypoint.sh mysq…"   About an hour ago   Up 5 minutes (healthy)   3306/tcp, 33060/tcp   mysql1
</pre>
    <p><code>$docker logs mysql1</code></p> 
    <p><code>$docker logs mysql1 2>&1 | grep GENERATED</code></p>
    <pre>GENERATED ROOT PASSWORD: ytEP3RIp@h3mulmIl4x#@x3wKUL=</pre>
    <p>The mysql server is up an running with generated root/password</p>
    <h4>Start mysql client:</h4>
    <p><code>$docker exec -it mysql1 mysql -uroot -p</code></p>
    <pre>Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 76
Server version: 8.0.17
Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql&gt;</pre>
<h4>Change root password:</h4>
<p><code>mysql&gt; ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';</code></p>
 <pre>Query OK, 0 rows affected (0.17 sec)</pre> 
 <pre>mysql&gt;create database test;
mysql&gt;CREATE USER 'test_user'@'%' IDENTIFIED BY 'test_user';
mysql&gt;GRANT ALL PRIVILEGES ON *.* TO 'test_user'@'%';
</pre>
 <h4>Start the bash shell within the container mysql1<h4>
  <p><code>$ docker exec -it mysql1 bash </code></p>
  <pre>bash-4.2# </pre>
  <h4>Run the shell command</h4>
  <p><code>bash-4.2# ls /var/lib/mysql</code></p>
  <pre>#innodb_temp   ca.pem		ibdata1		 performance_schema  undo_001
auto.cnf       client-cert.pem	ibtmp1		 private_key.pem     undo_002
binlog.000001  client-key.pem	mysql		 public_key.pem
binlog.000002  ib_buffer_pool	mysql.ibd	 server-cert.pem
binlog.index   ib_logfile0	mysql.sock	 server-key.pem
ca-key.pem     ib_logfile1	mysql.sock.lock  sys
</pre>
  <h4>Stop the container mysql1</h4>
  <p><code>$ docker stop mysql1</code></p>
  <pre>mysql1</pre>
  <h4>Start the container mysql1</h4>
  <p><code>$ docker start mysql1</code></p>
  <pre>mysql1</pre>
  <h4>Restart the container mysql1</h4>
  <p><code>$ docker restart mysql1</code></p>
  <pre>mysql1</pre>
  <h4>To delete the MySQL container, stop it first, and then use the docker rm command:</h4>
  <p><code>$ docker stop mysql1</code></p>
  <p><code>$ docker rm mysql1</code></p>  
  </section>
   <section>
     <h4>Docker Network</h4>
     <p><code>$ docker network list</code></p>
     <pre>NETWORK ID          NAME                DRIVER              SCOPE
d6aca9e061a2        bridge              bridge              local
8029d52bdce8        host                host                local
fb59ee8ce51c        none                null                local
</pre>
     <h4> Add a new Network</h4>
     <p><code>$ docker network create mysqlNetwork</code></p>
     <pre>71a1005c9d8c0440a5856a1ab74c505bd327f33d3c4222ec59912ae6cdae4735</pre>
     <h4>List the network</h4>
     <p><code>$ docker network list</code></p>
     <pre>NETWORK ID          NAME                DRIVER              SCOPE
d6aca9e061a2        bridge              bridge              local
8029d52bdce8        host                host                local
71a1005c9d8c        mysqlNetwork        bridge              local
fb59ee8ce51c        none                null                local
</pre>
     <h4>Inspect a particular network using ID or Name</h4>
     <p><code>$ docker network inspect mysqlNetwork</code></p>
     <pre>[
    {
        "Name": "mysqlNetwork",
        "Id": "71a1005c9d8c0440a5856a1ab74c505bd327f33d3c4222ec59912ae6cdae4735",
        "Created": "2019-07-28T17:15:42.012206203+04:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
</pre>
   </section>
    
</body></html>
