# comandi da linea di comando con lo script "lgtv.py"
Lo script è tratto e riadattato dalle seguenti fonti: http://harizanov.com/2013/12/control-lg-smart-tv-over-the-internet-using-a-raspberry-pi/; 

cambiare utente in "homeassitant"

sudo su -s /bin/bash/ homeassistant

cd /svr/homeassistant/homeassistant_venv/

sudo nano lgtv.py

incollare il contenuto dello script lgtv.py presente in questo progetto

chmod a+x lgtv.py

per lanciare comandi:

python3 lgtv.py [numero comando]

## comandi utili:

Un elenco completo è all'indirizzo http://developer.lgappstv.com/TV_HELP/index.jsp?topic=%2Flge.tvsdk.references.book%2Fhtml%2FUDAP%2FUDAP%2FAnnex+A+Table+of+virtual+key+codes+on+remote+Controller.htm

dare un'occhiata anche a questo elenco comandi: https://github.com/ubaransel/lgcommander/issues/9#issuecomment-135969965

1 - spegne la TV

24 - Volume up

25 - Volume down

26 - Mute (toggle)

27 - Channel UP (+)

28 - Channel DOWN (-)

# timer di spegnimento

## PROGETTO 1:
===========
### 1.a) Pulsante di spegnimento;
### 1.b) Creare una "card" con un timer spegnimento (creare automazione che spegne la tv oltre una certa soglia impostabile di utilizzo)

Il punto 1.a) l'ho ottenuto inserendo in conf.yaml:

switch:
  platform: command_line
  switches:
    lgtv_poweroff:
      command_off: "python3 /srv/homeassistant/homeassistant_venv/lgtv.py 1"
      friendly_name: TV Salone

Lo stesso risultato si può ottenere da:
shell_command:
  lgtv_timer_poweroff: python3 /srv/homeassistant/homeassistant_venv/lgtv.py 1

oppure invocando lo stesso servizio da developer tools

per il punto 1.b) si può partire dall'automazione:
