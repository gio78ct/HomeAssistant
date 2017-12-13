Tratto da: https://github.com/samabsalom/Home-Assistant-Config/blob/packages/packages/rebootpi.yaml

####### before this works run from cli --- sudo su -s /bin/bash hass then ssh-keygen press enter for all then ssh-copy-id pi@127.0.0.1
shell_command:
  rebootpi: ssh pi@127.0.0.1 sudo reboot

script:
  reboot_pi:
    alias: Reboot the Pi
    sequence:
      - service: shell_command.rebootpi

switch:
  - platform: wake_on_lan
    name: router
    mac_address: "dc:9f:db:29:a0:bc"
    host: 10.10.10.1

automation:
  - alias: reboot pi if connection lost to router
    trigger:
      platform: state
      entity_id: switch.router
      to: 'off'
      for: 
        minutes: 5
    action:
      - service_template: notify.pushbullet
        data_template:
          message: "This was done because HA lost connection to the router"
          title: "REBOOT"
      - service_template: notify.kodi
        data_template:
          message: "This was done because HA lost connection to the router"
          title: "REBOOT"
      - service: homeassistant.turn_on
entity_id: script.reboot_pi
