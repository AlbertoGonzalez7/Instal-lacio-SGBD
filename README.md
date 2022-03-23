# Instal-lacio-SGBD MySQL Percona Server
# PART 1 - Alberto Gonzalez i David Gil.

![percona logo](https://user-images.githubusercontent.com/101892290/159756334-cd8dacc6-2811-44b4-b46f-c83616fa32d8.jpg)

# Instalació
*Primer, haurem de esborrar el system profile localment amb les seguents comandes*

![WhatsApp Image 2022-03-17 at 17 18 15](https://user-images.githubusercontent.com/101892290/159757683-a0466728-69e0-4456-aaac-888d449a129f.jpeg)
![WhatsApp Image 2022-03-17 at 17 18 39](https://user-images.githubusercontent.com/101892290/159757870-b9c8cb08-d490-41e8-82bd-3f9ad509d855.jpeg)

*I després, registrar-se i subscriure:*

> subscription-manager register (posar usuari i password del compte)

> subscription-manager refresh

> subscription-manager attach --auto

![WhatsApp Image 2022-03-17 at 17 22 01](https://user-images.githubusercontent.com/101892290/159759364-954c8b4a-b98b-46c3-b115-e6f9353abe71.jpeg)
![WhatsApp Image 2022-03-17 at 17 23 53](https://user-images.githubusercontent.com/101892290/159762112-7e5b2b1c-74d9-49a9-86e2-1b55dc222d9f.jpeg)

*Ara, farem un update per detectar possibles paquets a instal·lar*

> sudo yum -y update

![sudo yum -y update](https://user-images.githubusercontent.com/101892290/159760412-2a0563d6-2b6d-40cb-b3f2-698885991233.jpg)

*Ara, instalarem el repositori Percona amb la seguent comanda*

> sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

![yum repositorios](https://user-images.githubusercontent.com/101892290/159761562-e393c194-8452-4b53-8940-8bad998998c8.jpg)

*Habilitem el servei Percona Server*

> sudo percona-release setup ps80

![WhatsApp Image 2022-03-23 at 18 42 37](https://user-images.githubusercontent.com/101892290/159762628-6df8f6cd-f00d-48ea-bc4f-e44aa720dba3.jpeg)

*Instalarem el Percona Server*

> sudo yum install percona-server-server

![percona server server](https://user-images.githubusercontent.com/101892290/159762891-27988fa3-e317-45de-a27a-8573cecb9876.jpg)

*Iniciem el servei*

> sudo service mysql start

![sudo service mysql start](https://user-images.githubusercontent.com/101892290/159763124-8f3d32ee-8afc-4efc-bfd0-7dc2fedd73b8.jpg)

*Haurem de afegir el port 3306 al firewall*

>sudo firewall-cmd --zone=public --add-port=3306/tcp --permanent success

>firewall-cmd --reload

![firewall](https://user-images.githubusercontent.com/101892290/159763613-f46d00d9-2823-471b-af95-2dba8b88524c.jpg)

# RESPON O COMPROVA ELS SEGÜENTS APARTATS
## 1. Un cop realitzada la instal·lació realitza una securització de la mateixa. Quin programa realitza aquesta tasca? Realitza una securització de la instal·lació indicant que la contrasenya de root sigui patata.

*Primer, executem la seguent comanda per que el servei mysqld s'inicii al inici del sistema*

> sudo systemctl enable --now mysqld

![sudo systemctl](https://user-images.githubusercontent.com/101892290/159764271-4377e92e-e36e-43bb-ad53-d864cafb156c.jpg)

*Després, executarem la seguent comanda per veure la contrasenya actual del root*

> sudo grep "temporary password" /var/log/mysqld.log

![sudo grep](https://user-images.githubusercontent.com/101892290/159765139-a0f94334-1459-46d6-ad1b-030d34f53419.PNG)

*Entrem en la base de dades amb la seguent comanda i entrem amb la contrasenya que ens ha sortit abans*

> mysql -u root -p

![WhatsApp Image 2022-03-23 at 18 58 53](https://user-images.githubusercontent.com/101892290/159765464-c3a084d9-a107-4bf9-bb49-0f97de353650.jpeg)

*D'acord, una vegada dins, per cambiar la contrasenya a 'patata' hem de executar la seguent comanda*


