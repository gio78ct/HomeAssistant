DUCKDNS:
Dalla versione 0.55 esiste il componente "duckdns".
https://home-assistant.io/components/duckdns/
Attivare il componente in luogo dell'installazione. 
Esso si occuperà anche di rinnovare automaticamente i certificati di LET'S ENCRYPT ogni 90 giorni.
https://www.splitbrain.org/blog/2017-08/10-homeassistant_duckdns_letsencrypt

GUIDA per AIO installaer (H.A. gira su virtualenv)
Set all this up via the pi user using sudo. Once you get to the point of creating the hook.sh file, you must make it executable. Then, change ALL permissions for ownership over to homeassistant for the entire dehydrated directory. sudo chmod -R homeassistant:homeassistant dehydrated/
You will ALSO need to add the cronjob to the homeassistant user because the pi user will not have permissions to the hook.sh. If you are a vi user like me, running a crontab -e as the HA user will put you in nano so if you don't know nano, just follow the on screen options while saving and editing. 
