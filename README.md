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

## NGINX reverse proxy
https://community.home-assistant.io/t/homeassistant-nginx-ssl-proxy-setup/53

Potrebbe eddere utile https://deviantengineer.com/2015/05/nginx-reverseproxy-centos7/


## TV LG-47LA660S
Vedi la guida "TV_LG_LA660S.md"

## MQTT - Mosquitto
In debian scretch non era installabile facilmente. Ho dovuto dare "aptitude install" invece di "apt install", seguito da vari "n" finchè la procedura non mi proponeva di installare dipendenze e applicazione aggiornati.
Poi ho seguito la guida https://www.youtube.com/watch?v=AsDHEDbyLfg

## Geofencing
Devices that are in the zone ‘Home’ will not appear on the map in the Home Assistant UI.

## Notifiche quando HA è offline
1. (Basato su google sheets e google calendar per gli SMS)
https://www.labnol.org/internet/website-uptime-monitor/21060/ 
2. (basato su www.uptimerobot.com e IFTTT, non so se possibile SMS…)
https://ifttt.com/applets/65431405d-get-if-notifications-when-uptimerobot-com-detects-the-server-is-down-when-it-s-back-online

A prima prova, il metodo 2 sembra essere meglio: ho messo h.a. offline ed ho subito ricevuto la notifica tramite l’app per android IFTTT

## Wake On Lan switch
https://home-assistant.io/components/switch.wake_on_lan/ (viene anche spiegato come si fa a eseguire comandi su un dispositivo remoto tramite ssh)

## SONOFF relays
https://github.com/arendst/Sonoff-Tasmota

Per aggiornare, https://github.com/arendst/Sonoff-Tasmota/wiki/Upgrade
alternativa
https://github.com/KmanOz/KmanSonoff/blob/master/README.md

## Text To Speech (TTS)
Vorrei realizzare qualcosa del genere: https://philhawthorne.com/j-a-r-v-i-s-inspired-announcementgreeting-for-home-assistant/

Tutti i seguenti tentativi sono stati effettuati usando, come riproduttore, delle istanze "media_player.squeezebox".

Google tts dà problemi a causa dell'utilizzo di SSL. Da trovare una soluzion e (ngix server?).

Microsoft non supporta l'italiano (nonostante sembrerebbe il contrario, hass mi segnalava errori al file di configurazione).

Adesso proverò PicoTTS o SVOX Pico. Prova: qualità pessima e stesso rpoblema con SSL, sebbene sia un riconoscimento offline!!!
