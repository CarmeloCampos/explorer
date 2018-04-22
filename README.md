******************************************
*** Install Repositorios
******************************************
sudo apt-get install build-essential libssl-dev libdb++-dev libboost-all-dev libqrencode-dev miniupnpc libminiupnpc-dev autoconf pkg-config libtool autotools-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev automake -y

Install git and nano
sudo apt-get install nano git -y

Update Packages
sudo apt-get update
sudo apt-get upgrade -y

******************************************
*** Setting up the Explorer
*** https://github.com/CarmeloCampos/explorer
******************************************

Install MongoDB Community Edition
https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update
sudo apt-get install -y mongodb-org

Default init system is systemd which was Upstart previously. So you need to install Upstart, reboot your system and here you go, you can now run mongodb service.

Install Upstart
sudo apt-get install upstart-sysv -y

Reboot your system
sudo reboot
sudo service mongod start

Running MongoDB - reference
sudo service mongod start
sudo service mongod stop
sudo service mongod restart

Installing Nodejs
sudo apt-get update
sudo apt-get install nodejs nodejs-legacy -y
sudo apt-get install npm -y

Creating a MongoDB Database
sudo mongo
> use explorerdb
> db.createUser( { user: "explorer", pwd: "password", roles: [ "readWrite" ] } )
> exit

Installing the Explorer
cd
git clone https://github.com/CarmeloCampos/explorer explorer
cd explorer && npm install --production

Modify the Settings File
sudo nano settings.json

See if it's working
npm start

Update the databases
sudo node scripts/sync.js index update 

Install Forever to keep the js running
sudo npm install forever -g
sudo npm install forever-monitor

Start the Explorer
forever start bin/cluster

******************************************
*** Installing Cron
*** https://help.ubuntu.com/community/CronHowto
******************************************

sudo apt-get install gnome-schedule -y

Editing Cron
sudo crontab -e

Add Cron to File to update the explorer
*/1 * * * * cd /path/to/explorer && /usr/bin/node scripts/sync.js index update > /dev/null 2>&1

Add Cron to make sure the Pulsed runs (NOT WORKING)
If anyone has a good reboot for this, please post in the comments.
@reboot cd /root/Pulse/src ./pulsed -daemon -txindex
@reboot cd /root/explorer forever start bin/cluster 
