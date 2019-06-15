# Mincraft Serer setup on PI

1. I used OpenJDK `sudo apt-get install -y galternatives openjdk-8-jdk` not Oracle JDK 
2. Then followed this guide https://www.linuxnorth.org/minecraft/


I gave found minetest all for OpenSource
`sudo apt-get install minetest-server` installs v 4 we want v 5

## This needs to be manually downloaded
https://forum.minetest.net/viewtopic.php?f=42&t=21723

* Install dependencies package: `sudo apt-get install libhiredis-dev libpq-dev`
* get build: `wget http://www.nathansalapat.com/downloads/5.0.tar.gz`
* extract build: `tar xvzf 5.0.tar.gz`
* Run: `EXTRACTEDFOLDER/bin/./minetestserver`

## That worked but SNAP may be better

* `sudo apt-get install snapd` or `sudo dnf install snapd` depending on your distro
* reboot
* `sudo snap install minetest`
* For the server run: `minetest --server`
* You may need to do this to fix permissions in terms of logging: `sudo chmod a+w /var/log/minetest`
* For the client run: `minetest`

## A rudementary file to start the server

* create a mineserver.sh file and populate with
`#!/bin/bash -x

minetest --server  --gameid minetest --worldname world &`

* `chmod +x mineserver.sh`
* `./mineserver.sh`


## Where to add the mods
* `cp -r [mod] ~/snap/minetest/current/.minetest/mods/`
* enable mod in /snap/minetest/current/worlds/world/world.mt file by adding load_mod_[modname]=true
* restart server

## TODO
make mineserver work with systemctl
