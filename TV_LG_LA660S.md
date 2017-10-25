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

oppure invocando lo stesso servizio da developer tools.

Per il punto 1.b) ho avuto qualche difficoltà. Era necessario "passare" il numero di minuti impostati con INPUT_NUMBER.TV_MINUTES come valore TEMPLATE per il DELAY prima di invocare il vero e proprio comando di spegnimento. Dalla documentazione, sembrerebbe che non è possibile passare template per il DELAY all'interno delle AUTOMATIONS. Ho quindi inserito tale "delay template" direttamente nello script che spegne la tv.

input_number:
  tv_minutes:
    name: minuti
    initial: 20
    min: 10
    max: 120
    step: 10

#- id: timer_lgtv_salone
- alias: "Timer TV LG Salone"
  hide_entity: True
  initial_state: 'on'
  trigger:
    platform: state
    entity_id: input_number.tv_minutes
  action:
    - service: script.timer_tv_script
    - service: persistent_notification.create
      data_template:
        message: "Impostato timer di spegnimento fra {{ (states.input_number.tv_minutes.state | int) }} minuti"
        title: "TV LG Salone"
      
timer_tv_script:
  alias: 'script timer tv'
  sequence:
     #- service: persistent_notification.create
      #data:
        #message: "avviso 1: lo script è stato invocato"
        #title: "timer_lgtv"
    - delay: '00:{{ states.input_number.tv_minutes.state | int }}:00'
    #- service: persistent_notification.create
      #data:
        #message: "avviso 2: il delay dello script ha funzionato"
        #title: "timer_lgtv"
    - service: shell_command.lgtv_timer_poweroff
    - delay: '00:00:03'
    - service: shell_command.lgtv_timer_poweroff
    #- service: persistent_notification.create
      #data:
        #message: "avviso 3: lo shell_command è stato innescato"
        #title: "timer_lgtv"
 
