#DUCKDNS:
Dalla versione 0.55 esiste il componente "duckdns".
https://home-assistant.io/components/duckdns/
Attivare il componente in luogo dell'installazione. 
Esso si occuperà anche di rinnovare automaticamente i certificati di LET'S ENCRYPT ogni 90 giorni.
https://www.splitbrain.org/blog/2017-08/10-homeassistant_duckdns_letsencrypt

GUIDA per AIO installer (H.A. gira su virtualenv)
Set all this up via the pi user using sudo. Once you get to the point of creating the hook.sh file, you must make it executable. Then, change ALL permissions for ownership over to homeassistant for the entire dehydrated directory. sudo chown -R homeassistant:homeassistant dehydrated/
You will ALSO need to add the cronjob to the homeassistant user because the pi user will not have permissions to the hook.sh.
sudo su -s /bin/bash homeassistant
crontab -e
come ultima riga incollare: 
0 1 1 * * /home/homeassistant/dehydrated/dehydrated -c

#Reconfigure HomeAssistant

Edit your configuration.yaml and add the new certificate to the http section:

configuration.yaml
http:
  api_password: !secret hass_pass
  ssl_certificate: /home/pi/dehydrated/certs/gio78.duckdns.org/fullchain.pem
  ssl_key: /home/pi/dehydrated/certs/gio78.duckdns.org/privkey.pem
  base_url: gio78.duckdns.org:8123
