# Docker-etc

cd ~
ll
mkdir HW5
cd HW5
nano docker-compose.yaml


version: ‘3.9’


services:


  db:
	image: mariadb:10.10.2
	environment:
  	  MYSQL_ROOT_PASSWORD: 12345
	deploy:
  	  mode: replicated
  	  replicas: 2
 
  adminer:
	image: adminer:4.8.1
	restart: always
	ports:
  	  - 6080:8080
	deploy:
  	  mode: replicated
  	  replicas: 1


sudo docker compose up
sudo docker compose start -d
sudo docker compose down
udo docker compose up -d
sudo docker ps
history
