******************************************
Instalar Repositorios
=====================
******************************************
Escribir en la terminal los siguientes comandos:

```bash
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install build-essential libssl-dev libdb-dev unzip libdb++-dev libboost-all-dev git libssl1.0.0-dbg libdb-dev libdb++-dev libboost-all-dev libminiupnpc-dev libevent-dev libcrypto++-dev libgmp3-dev git npm nodejs-legacy curl build-essential libtool autotools-dev autoconf pkg-config libssl-dev redis-server libdb++-dev libboost-all-dev libqrencode-dev miniupnpc libminiupnpc-dev pkg-config libtool autotools-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev automake -y
```

******************************************
Instalar git y nano
---------------------
******************************************
Escribir en la terminal los siguientes comandos:

```bash
sudo apt-get install nano git -y
```

******************************************
Paquetes de actualización
---------------------
******************************************
Escribir en la terminal los siguientes comandos:

```bash
sudo apt-get update
sudo apt-get upgrade -y
```

******************************************
La adición de la Moneda
---------------------
******************************************
Escribir en la terminal los siguientes comandos:
```bash
sudo git clone https://github.com/WolfClover/clovercoin-source/
```

Cambie los Directorios src/
---------------------
******************************************
```bash
cd clovercoin-source/src/ 
```

Compilar el código
---------------------
******************************************
```bash
sudo make -f makefile.unix RELEASE=0
sudo chmod +x clovercoind
```

Inicie el archivo con el daemon, de modo que usted puede crear un archivo de configuración
---------------------
******************************************
```bash
sudo ./clovercoind -daemon
```

Crear un fichero de configuración .clovercoin/clovercoin.conf
---------------------
******************************************
```bash
cd
sudo nano .clovercoin/clovercoin.conf
```

rpcuser=rpc_clovercoin
rpcpassword=57fca2b6e28491f9ceaa56aba
rpcallowip=127.0.0.1
rpcport=36600
listen=1
server=1
txindex=1
daemon=1
addnode=node.wolfclover.com

Asegúrese de que el archivo de sólo lectura.
---------------------
******************************************
```bash
sudo chmod 400 .clovercoin/clovercoin.conf
cd clovercoin-source/src/
sudo ./clovercoind -daemon -txindex
```

Compruebe que el demonio ha comenzado. Si devuelve información, el demonio está trabajando!
---------------------
******************************************
```bash
sudo ./clovercoind getinfo
```

Detener el daemon
---------------------
******************************************
```bash
sudo ./clovercoind stop
```

******************************************
*** La configuración del Explorador
---------------------
******************************************
*** https://github.com/CarmeloCampos/explorer
******************************************

Instalar MongoDB Edición De La Comunidad
https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

Init predeterminado del sistema es systemd que fue Advenedizo anteriormente. Por lo que necesita para instalar Advenedizo, reinicie el sistema y aquí usted vaya, usted puede ahora ejecutar el servicio de mongodb.

Instalar Upstart (opcional)
```
sudo apt-get install upstart-sysv -y
```

Reinicie el sistema
```
sudo reboot
sudo service mongod start
```

Ejecución de MongoDB - referencia
```
sudo service mongod start
sudo service mongod stop
sudo service mongod restart
```

La Instalación De Nodejs
```
sudo apt-get update
sudo apt-get install nodejs nodejs-legacy -y
sudo apt-get install npm -y
```

La creación de una Base de datos MongoDB
```
sudo mongo
> use explorerdb
db.createUser( { user: "explorer", pwd: "password", roles: [ "readWrite" ] } )
> exit
```

Instalar el Explorer
```
cd
git clone https://github.com/CarmeloCampos/explorer explorer
cd explorer && npm install --production
```

Modificar el Archivo de Configuración
```
sudo nano settings.json
```

A ver si funciona
```
npm start
```

Actualización de las bases de datos
```
sudo node scripts/sync.js index update 
```

Instale para Siempre para mantener el js ejecutando
```
npm conf set strict-ssl false
sudo npm install forever -g
sudo npm install forever-monitor
```

Inicie el Explorador para siempre
```
forever start bin/cluster
```

******************************************
*** La Instalación De Cron
*** https://help.ubuntu.com/community/CronHowto
******************************************

```
sudo apt-get install gnome-schedule -y
```

Edite Cron
```
sudo crontab -e
```

Agregar Cron para Archivo para actualizar el explorer
*/1 * * * * cd /path/to/explorer && /usr/bin/node scripts/sync.js index update > /dev/null 2>&1

Agregar Cron para asegurarse de que los Impulsos se ejecuta (NO de TRABAJO)
Si alguien tiene un buen reinicio para esto, por favor, publicarlo en los comentarios.
@reboot cd /root/Pulse/src ./pulsed -daemon -txindex
@reboot cd /root/explorer forever start bin/cluster 
