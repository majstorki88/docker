# docker

pokrenuti docker-compose.yml koji će kreirati okruženje sa NGINX load balanserom, 3 Tomcat web servera i bazni MySQL kontjener

OS na kome je instaliran Docker - CentOS 7 x64

PREREQUISITES - instaliran Docker-engine i docker-compose na mašini host-a
Instalacija:

DOCKER ENGINE

1.	Instalacija zahtevanih paketa. yum-utils sa yum-config-manager dodatkom, i device-mapper-persistent-data i lvm2 su zahtevani zbog devicemapper driverom za storage.

$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2

2.	Setovanje stabilnog repositorijuma. Stabilni repositorijum je neophodan i ako se koristi testni ili edge repostitorijum sa najnovijim update-ima

$ sudo yum-config-manager \
--add-repo \
https://download.docker.com/linux/centos/docker-ce.repo

3.	Update-ovanje yum paketskog indeksa.

$ sudo yum makecache fast

4.	Instalacija posledlje verzije docker-a.

$ sudo yum install docker-ce

U koliko se ne navede verzija, sa yum install i yum update se instalira poslednja verzija

5.	Start Docker.

$ sudo systemctl start docker

6.	Verifikovati da je docker pravilno instaliran pokretanjem hello-world image-a.

$ sudo docker run hello-world

DOCKER COMPOSE

1. Instalacija docker compose se vrsi komandom

sudo yum install docker-compose

SETOVANJE ENVIRONMENTA

1. kreirati home direktorijum docker-a

$ sudo mkdir /home/docker/projekat

2. setobati permisije i vlasnika da bude ROOT ili user koji run-uje docker engine proces

$ sudo chmod +x -R /home/docker/projekat
$ sudo chown root:root /home/docker/projekat

3. U home direktorijumu docker-a klonirati git repozitorijum

$ sudo su
$ cd /home/docker/projekat
$ git clone https://github.com/majstorki88/docker

PODIZANJE OKRUZENJA

1. U folderu /home/docker/projekat pokrenuti komandu docker-compose -f docker-compose.yml up

Nakon uspesnog izvrsenja dobijate 5 kontejnera - NGINX load balanser, 3 tomcate-a sa zahtevanom aplikacijom i MySQL bazom
