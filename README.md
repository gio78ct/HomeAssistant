# [HomeAssistant](https://home-assistant.io)
Use [HASSCTL](https://github.com/dale3h/hassctl) to have some of these super simple commandline shortcuts for starting, stopping, upgrading, and debugging HA.
Don't forget to modify the configuration file "/etc/hassctl.conf" according to your type of H.A. installation (Hassbian, AIO, Hass.io, ecc).
```
hassctl update-hass
hassctl start
hassctl stop
hassctl error
hassctl log - Follow the Home Assistant logs (errors are highlighted)
hassctl zwave - Follow the Open Z-Wave logs
```
## USEFUL LINKS
* http://www.yamllint.com (tool to verify *.yaml sintax)
* https://materialdesignicons.com/

# All In One Installation
https://www.nicolapreo.it/installare-home-assistant/

## Dynamic DNS: duckdns.org
A partire dalla vers. 0.55 è integrato in HomeAssistant come componente; lo stesso gestisce anche la creazione e il rinnovo automatico dei certificati SSL di Let's Encrypt.
Vedi il documento "HomeAssistant/DUCKDNS_LETSENCRYPT.md" 


## SSL: Let's Encrypt
Vedi sopra "Dynamic DNS: duckdns.org"

## TV LG-47LA660S
Vedi la guida "TV_LG_LA660S.md"
