# Instal-lacio-SGBD MySQL Percona Server
# PART 1 - Alberto Gonzalez

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

![WhatsApp Image 2022-03-23 at 19 07 07](https://user-images.githubusercontent.com/101892290/159766839-1cdfb766-6cbe-458e-8e92-f46ec55f1806.jpeg)

*Pero com podem observar dona error i ens diu que ho hem de fer amb un ALTER USER, pero si ho fem amb ALTER USER ens dira que la contrasenya no compleix els requisits minims, llavors, primer hem de cambiar la contrasenya a una que si compleixi aquests requisits minims (P@ssw0rd) i llavors si ens deixara cambiar la longitud mínima de la contrasenya i la seguretat a LOW.*

![WhatsApp Image 2022-03-23 at 19 08 07](https://user-images.githubusercontent.com/101892290/159767000-cd5b8469-e153-4f96-aaaf-76f700521255.jpeg)

*I un cop fet aixo, ja ens deixara canviar la contrasenya a patata*

![WhatsApp Image 2022-03-23 at 19 09 13](https://user-images.githubusercontent.com/101892290/159767194-42fa8b06-d51c-4253-b9c5-05e7e659029d.jpeg)

*Politica de les contrasenyes despres de fer els passos anteriors*

![WhatsApp Image 2022-03-22 at 16 32 37](https://user-images.githubusercontent.com/101892290/159767515-4f950072-f1e0-40a3-bf2e-34f00164b6ea.jpeg)

*I configurem el mysql secure installation*

> mysql_secure_installation

![WhatsApp Image 2022-03-22 at 16 35 54](https://user-images.githubusercontent.com/101892290/159767746-3284ecd2-2495-4779-895a-0cccd5e0a4b9.jpeg)

## 2. Quines són les instruccions per arrancar / verificar status / apagar servei de la base de dades de Percona Server en el sistema operatiu?

*Arrancar servei*

> sudo service mysql start

*Verificar status servei*

> sudo service mysql status

![sudo service mysql start](https://user-images.githubusercontent.com/101892290/159768444-4decd58e-618e-4d98-8942-4d474e3d9b62.jpg)


*Apagar servei*

>sudo service mysql stop

![WhatsApp Image 2022-03-23 at 19 17 27](https://user-images.githubusercontent.com/101892290/159768556-6303cd2a-01ae-4bec-b477-b221e590a68b.jpeg)

## 3. A on es troba i quin nom rep el fitxer de configuració del SGBD Percona Server?

*El fitxer de configuració del SGBD Percona Server es troba en la ruta /etc/my.cnf*

>Es pot entrar amb nano /etc/my.cnf

![mycnf nano](https://user-images.githubusercontent.com/101892290/159769167-022d4e36-f359-4b02-96f3-806088a0e5ec.jpg)

## 4. A on es troben físicament els fitxers de dades (per defecte). Com ho has sabut?

*En la ruta /var/lib/mysql. Ho indica en la documentació oficial de Precona*

> ls /var/lib/mysql.

![var lib mysql](https://user-images.githubusercontent.com/101892290/159769439-231b21de-931a-4a32-888e-fed3d0987e0d.jpg)

## 5. Crea un usuari anomenat asix en el sistema operatiu i en SGBD de tal manera que aquest usuari del sistema operatiu no hagi d'introduir l'usuari i password cada vegada que cridem al client mysql? ##
#### Usuari SO-→ asix / patata ####
#### Usuari MySQL → asix / patata ####

*En la base de dades, crearem l'usuari amb permis total amb les seguents comandes*

![create user asix](https://user-images.githubusercontent.com/101892290/159769978-000822c3-e97f-4c25-845d-9df4bef0b506.jpg)

*Creem l'usuari en el sistema*

> sudo useradd asix

![sudo useradd asix](https://user-images.githubusercontent.com/101892290/159770234-50bfbdc5-2b5c-43ac-9ae1-b560fd632959.jpg)

*Canviem la contrasenya a patata*

> sudo passwd asix

![sudo passwd asix](https://user-images.githubusercontent.com/101892290/159770443-67ae3fcf-12e5-41c6-924b-56940d438dac.jpg)

*Afegirem al arxiu /etc/my.cnf l'usuari asix i la seva contrasenya*

> entrem amb nano /etc/my.cnf

![nano etc asix ponerlo](https://user-images.githubusercontent.com/101892290/159770610-95e2d502-081c-418d-9fc6-418ada293b54.jpg)

*Comprovació de que pot entrar sense possar contrasenya*

> su asix i després mysql

![su asix](https://user-images.githubusercontent.com/101892290/159770818-5e2058ef-169d-4db2-9cf5-7eff590c599d.jpg)

## 6. El servei de MySQL (mysqld) escolta al port 3306. Quina modificació/passos caldrien fer per canviar aquest port a 33306 per exemple? Important: No realitzis els canvis. Només indica els passos que faries. ##

*Per modificar el port escolta 3306 al port 33306, primer hauriem d'aturar el servei amb la seguent comanda*

>sudo service mysql stop

*I després, al arxiu /etc/my.cnf posar els parametres seguents*

![puerto cambiarlo](https://user-images.githubusercontent.com/101892290/159771597-fab517de-7442-4f2a-9183-0cd1d1d768a8.jpg)


#### Links diversos (Sobre Percona).

> https://www.inmotionhosting.com/support/server/databases/edit-mysql-my-cnf/

> https://dev.mysql.com/doc/refman/8.0/en/password-security-user.html

> https://www.percona.com/doc/percona-server/LATEST/installation/post-installation.html

> https://www.percona.com/doc/percona-server/8.0/installation/yum_repo.html

> https://www.stackscale.com/es/blog/instalar-servidor-percona-sustituto-mysql/

> https://www.linuxhispano.net/2012/04/18/donde-almacena-los-datos-mysql/#:~:text=El%20lugar%20suele%20ser%3A%20%2Fvar,debemos%20mirar%20el%20fichero%20my.

#### Links diversos (Sobre GitHub).

> https://docs.github.com/es/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax

> https://www.youtube.com/watch?v=xmK1Q5uzH4w
