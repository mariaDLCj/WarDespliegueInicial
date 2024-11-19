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
