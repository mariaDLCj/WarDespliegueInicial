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

Error 
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo nano /etc/systemd/system/tomcat.service
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo nano /etc/systemd/system/tomcat.service
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo nano /etc/systemd/system/tomcat.service
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo nano /etc/systemd/system/tomcat.service
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo systemctl daemon-reload
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo systemctl enable tomcat
Created symlink /etc/systemd/system/multi-user.target.wants/tomcat.service → /etc/systemd/system/tomcat.service.
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo system start tomcat
sudo: system: orden no encontrada
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo systemctl start tomcat
Job for tomcat.service failed because the control process exited with error code.
See "systemctl status tomcat.service" and "journalctl -xeu tomcat.service" for details.
root@usuario-VirtualBox:/usr/tomcat10/bin# sudo systemctl status tomcat.service
× tomcat.service - Apache Tomcat 10 Web Application Container
     Loaded: loaded (/etc/systemd/system/tomcat.service; enabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Tue 2024-11-19 14:33:05 CET; 20s ago
    Process: 94221 ExecStart=/usr/tomcat10/bin/startup.sh (code=exited, status=217/USER)
        CPU: 2ms

nov 19 14:33:05 usuario-VirtualBox systemd[1]: Starting Apache Tomcat 10 Web Application Container...
nov 19 14:33:05 usuario-VirtualBox systemd[94221]: tomcat.service: Failed to determine user credentials: No such process
nov 19 14:33:05 usuario-VirtualBox systemd[94221]: tomcat.service: Failed at step USER spawning /usr/tomcat10/bin/startup.sh: No such process
nov 19 14:33:05 usuario-VirtualBox systemd[1]: tomcat.service: Control process exited, code=exited, status=217/USER
nov 19 14:33:05 usuario-VirtualBox systemd[1]: tomcat.service: Failed with result 'exit-code'.
nov 19 14:33:05 usuario-VirtualBox systemd[1]: Failed to start Apache Tomcat 10 Web Application Container.
root@usuario-VirtualBox:/usr/tomcat10/bin# 


CREATE DATABASE IF NOT EXISTS pruebasjava;

USE pruebasjava;

CREATE TABLE IF NOT EXISTS `aves` (
  `anilla` varchar(3) COLLATE utf8_spanish_ci NOT NULL,
  `especie` varchar(20) COLLATE utf8_spanish_ci NOT NULL,
  `lugar` varchar(30) COLLATE utf8_spanish_ci NOT NULL,
  `fecha` date NOT NULL,
  PRIMARY KEY (`anilla`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 COLLATE=utf8_spanish_ci;


INSERT INTO `aves` VALUES ('123','cigueña','En el campo','2024-05-09'),('AAS','Cormorán','En la playa','2024-10-10'),('ABC','Golondrina','En el tejado','2024-05-09');


