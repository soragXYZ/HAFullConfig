# HAFullConfig

## Flashing OS from external USB to internal eMMC
https://wiki.seeedstudio.com/ODYSSEY-X86-Home-Assistant/#run-home-assistant-from-external-hdd-ssd-m2-ssd-emmc

Download latest Ubuntu image and flash it on USB with Balena Etcher or sth:  
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

### Zigbee2MQTT
zigbee2MQTT: https://github.com/zigbee2mqtt/hassio-zigbee2mqtt  

Do not forget to change the default network key !!!  

https://www.zigbee2mqtt.io/advanced/zigbee/03_secure_network.html

### CloudFlared
https://github.com/brenner-tobias/ha-addons  

Change tunnel name, and add this to configuration.yaml:
```
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.30.33.0/24
```

### Google Drive for back ups
google drive: https://github.com/sabeechen/hassio-google-drive-backup

### Security
Configure MFA and ip ban

Modify configuration.yaml
```
http:
  ip_ban_enabled: true
  login_attempts_threshold: 4
```

### Monitor hardware
https://www.home-assistant.io/integrations/systemmonitor/  
https://community.home-assistant.io/t/is-it-possible-to-read-the-cpu-temperature-on-an-intel-nuc-running-hassos/198718  

Create a sensor.yaml file (for networking, it can be eth0, enp2s0 or sth else, check your hardware) 

```
- platform: systemmonitor
  resources:
    - type: disk_use_percent
      arg: /config
    - type: disk_use
    - type: disk_free
    - type: memory_use_percent
    - type: memory_use
    - type: memory_free
    - type: swap_use_percent
    - type: swap_use
    - type: swap_free
    - type: load_1m
    - type: load_5m
    - type: load_15m
    - type: network_in
      arg: enp2s0
    - type: network_out
      arg: enp2s0
    - type: throughput_network_in
      arg: enp2s0
    - type: throughput_network_out
      arg: enp2s0
    - type: packets_in
      arg: enp2s0
    - type: packets_out
      arg: enp2s0
    - type: ipv4_address
      arg: enp2s0
    - type: ipv6_address
      arg: enp2s0
    - type: processor_use
    - type: last_boot

- platform: command_line
  name: CPU Temperature
  command: "cat /sys/class/thermal/thermal_zone0/temp"
  unit_of_measurement: "°C"
  value_template: "{{ value | multiply(0.001) }}"
```

Add this line to configuration.yaml
```
sensor: !include sensor.yaml
```

### Themes and card
theme: waves 
card: minigraph card, mushroom, apexcard

### Database
mariaDb