test changes
down and upstream jobs
new view pipeline created

sudo useradd -c "Sonar System User" -d /opt/sonarqube -g sonar -s /bin/bash sonar
sudo unzip sonarqube-*.zip -d /opt
 sudo useradd -c "user to run SonarQube" -d /opt/sonarqube -g sonar sonar 
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube

LimitNOFILE=65536
LimitNPROC=4096

Devopsmentor@321
 sudo vi /etc/systemd/system/sonar.service

 ====================

mv sonarube-* /opt/
 useradd sonaradmin
 chown -R sonaradmin:sonaradmin /opt/sonarqube-*

 netstat -tulpn


6.	chown -R sonaruser sonaruser /opt/sonarqube-x.x  


this is sonar project