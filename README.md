## Home Assistant with hassio-ecoflow setup
sudo su <br>
apt install -y python3 python3-dev python3-venv python3-pip bluez libffi-dev libssl-dev libjpeg-dev zlib1g-dev autoconf build-essential libopenjp2-7 libtiff5 libturbojpeg0-dev tzdata git rsync <br>
#### Create user homeassistant and service directories <br>
useradd -rm homeassistant -G dialout,gpio,i2c <br>
mkdir /srv/homeassistant <br>
chown homeassistant:homeassistant /srv/homeassistant <br>
#### Switch user, install home assistant <br>
su -u homeassistant -H -s <br>
cd /srv/homeassistant <br>
python3 -m venv . <br>
source bin/activate <br>
python3 -m pip install wheel <br>
pip3 install homeassistant <br>
#### Start homeassistant <br>
hass <br>
#### Open local browser with adress http://localhost:8123/ <br>
#### Follow the process <br>
#### Close browser or clean cache in browser<br>
#### Stop hass; STRG + C in terminal <br>
#### Get hassio-ecoflow <br>
git clone https://github.com/vwt12eh8/hassio-ecoflow.git /home/homeassistant/hassio-ecoflow <br>
cp -r /home/homeassistant/hassio-ecoflow/custom_components /home/homeassistant/.homeassistant/ <br>
#### Start homeassistant again <br>
hass <br>
#### Open local browser again http://localhost:8123/ <br>
#### Try to add an Integration with name Ecoflow <br>
#### Start homeassistant at boot the dirty way
cat << EOF > /srv/homeassistant/start.sh <br>
cd /srv/homeassistant/  <br>
python3 -m venv .  <br>
source bin/activate  <br>
hass  <br>
EOF <br>
chmod 755 /srv/homeassistant/start.sh <br>
#### Insert following line in /etc/rc.local as root before exit 0 <br>
su - homeassistant -c "/srv/homeassistant/start.sh &" <br>
### ToDoes <br>
- Set up homeassistant as a systemd service <br>
- Set up homeassistant with ssl (If we run it only on local network over hotspot and use hotspot only for that it is relative secure atm) <br>
- Tutorial How to start with homeassistant website and app <br>
