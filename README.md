<Proxy balancer://tomcat-cluster>
    BalancerMember ajp://localhost:7009
    BalancerMember ajp://localhost:8009
    BalancerMember ajp://localhost:9009
    ProxySet lbmethod=byrequests
</Proxy>

ProxyPreserveHost On
ProxyPass /balancer-manager !
ProxyPass / balancer://tomcat-cluster/
ProxyPassReverse / balancer://tomcat-cluster/

<Location /balancer-manager>
    SetHandler balancer-manager
    Order deny,allow
    Allow from all
    Require host localhost
</Location>


proxy proxy_ajp lbmethod_byrequests proxy_balancer
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo nano /etc/systemd/system/tomcat.service

Voy a par en la ruta anterior qe estaba vacía lo siguiente:

[Unit]
Description=Apache Tomcat 10 Web Application Container
After=network.target

[Service]
Type=forking
Environment=JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
Environment=CATALINA_PID=/usr/tomcat10/temp/tomcat.pid
Environment=CATALINA_HOME=/usr/tomcat10
Environment=CATALINA_BASE=/usr/tomcat10
ExecStart=/usr/tomcat10/bin/startup.sh
ExecStop=/usr/tomcat10/bin/shutdown.sh
User=tomcat
Group=tomcat
Restart=always

[Install]
WantedBy=multi-user.target

