# HAFullConfig

## Flashing OS from external USB to internal eMMC
https://wiki.seeedstudio.com/ODYSSEY-X86-Home-Assistant/#run-home-assistant-from-external-hdd-ssd-m2-ssd-emmc

Download latest Ubuntu image and flash it on USB:  
https://ubuntu.com/download/desktop  

Plug it and boot from it  

Get HAOS and untar
```
wget https://github.com/home-assistant/operating-system/releases/download/XXX/haos_generic-x86-64-XXX.img.xz
unxz haos_generic-x86-64-XXX.img.xz
```

Check where to flash
```
lsblk
```

Flash
```
sudo dd if=haos_generic-x86-64-XXX.img of=/dev/sda status=progress
```

Reboot
```
sudo reboot
```

Then go to homeassistant.local:8123

## HA Basics config
set location

user -> activer mode avancée
add on install: SSH, mosquitto broker, studio code server

with SSH install HACS: wget -O - https://get.hacs.xyz | bash -
paramètres services -> HACS

zigbee2MQTT: https://github.com/zigbee2mqtt/hassio-zigbee2mqtt

cloudflared: https://github.com/brenner-tobias/ha-addons
changer nom tunnel
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.30.33.0/24

google drive: https://github.com/sabeechen/hassio-google-drive-backup

ajouter MFA et ban ip

monitor hardware: https://community.home-assistant.io/t/is-it-possible-to-read-the-cpu-temperature-on-an-intel-nuc-running-hassos/198718
https://www.home-assistant.io/integrations/systemmonitor/
replace eth0 by enp2s0

theme: waves 
card: minigraph card, mushroom, apexcard

changer database pour mariaDb