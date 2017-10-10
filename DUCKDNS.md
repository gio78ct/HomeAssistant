# DUCKDNS:
Dalla versione 0.55 esiste il componente "duckdns".
https://home-assistant.io/components/duckdns/
Attivare il componente in luogo dell'installazione. 
Esso si occuperà anche di rinnovare automaticamente i certificati di LET'S ENCRYPT ogni 90 giorni.
https://www.splitbrain.org/blog/2017-08/10-homeassistant_duckdns_letsencrypt

## GUIDA per AIO installer (H.A. gira su virtualenv)
Set all this up via the pi user using sudo.

Once you get to the point of creating the hook.sh file, you must make it executable.

# GENERARE I CERTIFICATI:
Time to run dehydrated.

First, register a new private key with letsencrypt:

$> ./dehydrated --register  --accept-terms

#INFO: Using main config file /home/homeassistant/dehydrated/config
 + Generating account key...
 + Registering account key with ACME server...
 + Done!
Then generate the certificate:

$ ./dehydrated -c

#INFO: Using main config file /home/homeassistant/dehydrated/config
Processing myhome.duckdns.org
 + Signing domains...
 + Generating private key...
 + Generating signing request...
 + Requesting challenge for myhome.duckdns.org...
OK
 + Responding to challenge for myhome.duckdns.org...
OK
 + Challenge is valid!
 + Requesting certificate...
 + Checking certificate...
 + Done!
 + Creating fullchain.pem...
 + Walking chain...
 + Done!
That's it. We now have a valid certificate!

AND NOW... Change ALL permissions for ownership over to homeassistant for the entire dehydrated directory

sudo chown -R homeassistant:homeassistant dehydrated/

## Automate Renewing

Let'sEncrypt certificates expire after 90 days, so we need to automatically renew them. We simply call dehydrated via cron on every 1st day of the month:

You will need to add the cronjob to the homeassistant user because the pi user will not have permissions to the hook.sh:

sudo su -s /bin/bash homeassistant

crontab -e

come ultima riga incollare: 
0 1 1 * * /home/pi/dehydrated/dehydrated -c

## Reconfigure HomeAssistant

Edit your configuration.yaml and add the new certificate to the http section:

configuration.yaml

http:

  api_password: !secret hass_pass
  
  ssl_certificate: /home/pi/dehydrated/certs/gio78.duckdns.org/fullchain.pem
  
  ssl_key: /home/pi/dehydrated/certs/gio78.duckdns.org/privkey.pem
  
  base_url: gio78.duckdns.org:8123

Change ALL permissions for ownership over to homeassistant for the entire dehydrated directory

sudo chown -R homeassistant:homeassistant dehydrated/
  
  Finally restart HomeAssistant

$> sudo service home-assistant restart

Your HomeAssistant should now be available via https://gio78.duckdns.org:8123.
