# docker

pokrenuti docker-compose.yml koji će kreirati okruženje sa NGINX load balanserom i 3 Tomcat web servera

OS na kome je instaliran Docker - CentOS 7 x64

PREREQUISITES - instaliran Docker-engine i docker-compose na mašini host-a
Instalacija:

DOCKER ENGINE

1.	Instalacija zahtevanih paketa. yum-utils sa yum-config-manager dodatkom, i device-mapper-persistent-data i lvm2 su zahtevani zbog devicemapper driverom za storage.
Instaliraju se sa komandom:

$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2

2.	Setovanje stabilnog repositorijuma. Stabilni repositorijum je neophodan i ako se koristi testni ili edge repostitorijum sa najnovijim update-ima
$ sudo yum-config-manager \
--add-repo \
https://download.docker.com/linux/centos/docker-ce.repo

3.	Opciono: Enable-ovanje edge i testnog repozitorijuma. Ovi repositorijumi već postoje u docker.repo u repostirorijumu koji smo instalirali sa tim sto su disableovani. Mogu se enable-ovati sledećim komandama bez uticaja na stabilni repositorijum:
$ sudo yum-config-manager --enable docker-ce-edge
$ sudo yum-config-manager --enable docker-ce-testing

4.	Možemo disable-ovati edge ili testni repositorijum pokretanjem yum-config-manager komande sa --disable parametrom. Ako želimo da ih ponovo enable-ujemo, koristićemo --enable parametar. Sledeća komanda disable-uje edge repository.
$ sudo yum-config-manager --disable docker-ce-edge
U našoj instalaciji, enable-ovani su ovi repositorijumi radi testiranja novih patsheva.

5.	Update-ovanje yum paketskog indeksa.
$ sudo yum makecache fast

6.	Instalacija posledlje verzije docker-a.
$ sudo yum install docker-ce
U koliko se ne navede verzija, sa yum install i yum update se instalira poslednja verzija

7.	Na produkcionim sistemima, bolja opcija je da se instalira konkretna verzija docker-a listanjem dostupnih verzija komandom list. Ovaj primer korisri sort -r parametar zbog sortiranja, od najvise do najnize i odsecen je opis. Ova yum list komanda prikazuje samo binarne pakete. Da bi se prikazali i izvorni paketi, potrebno je ukloniti .x86_64 iz imena paketa.
$ yum list docker-ce.x86_64  --showduplicates | sort -r

docker-ce.x86_64  17.06.0.el7                               docker-ce-stable  
Sadrzaj liste zavisi od repositorijuma koji su enable-ovani, i biće prikazani za verziju CentOS-a koja se koristi (.el7 sufiks za ovaj slučaj). Prva kolona je ime verzije. Druga kolona je verzija. Treca kolona je ime repositorijuma na kojem je instalacija. Radi instalacije željene verzije, u komandi koristiti ime verzije (prva kolona) i verziju (druga kolona) odvojenih crtom (-):
$ sudo yum install docker-ce-<VERSION>

8.	Start Docker.
$ sudo systemctl start docker
9.	Verifikovati da je docker pravilno instaliran pokretanjem hello-world image-a.
$ sudo docker run hello-world
