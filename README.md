# HAFullConfig

https://wiki.seeedstudio.com/ODYSSEY-X86-Home-Assistant/

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