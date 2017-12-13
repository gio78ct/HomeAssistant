Si può personalizzare quali "persistent notifications" far apparire in quali "schede" aggiungendo un "NOTIFICATION_ID" nell'apposita sezione di un'automazione. Viene così creata una ENTITY che può essere inserita dove serve nel file GROUPS.YAML

If you prefer a more silent approach then you could work with persistent notifications

#Under Group segment
group:
  default_view:
    view: yes
    entities:
      - persistent_notification.movie
      - persistent_notification.music
      - persistent_notification.occupants

#Under Automation segment
automation:
- alias: 'Announcement Movie state changed'
  hide_entity: true
  trigger:
    platform: state
    entity_id: media_player.kodi, media_player.kodi_bedroom, media_player.lg_tv
  action:
    service: persistent_notification.create
    data_template:
      message:  >
        {{ trigger.to_state.attributes.media_title }} is now {{ trigger.to_state.state }} in the {{ trigger.to_state.attributes.friendly_name }}.
      notification_id: "movie"

- alias: 'Announcement Music state changed'
  hide_entity: true
  trigger:
    platform: state
    entity_id: media_player.livingroom, media_player.bedroom
  action:
    service: persistent_notification.create
    data_template:
      message:  >
        {{ trigger.to_state.attributes.media_artist }} - {{ trigger.to_state.attributes.media_title }} is now {{ trigger.to_state.state }} in the {{ trigger.to_state.attributes.friendly_name }}.
      notification_id: "music"

Ah you want to know about the presence notication as well? Here you go with a nice timestamp added,

- alias: 'Occupants State Change Alert'
  hide_entity: true
  trigger:
    platform: state
    entity_id: device_tracker.kylo_ren, device_tracker.snoke, device_tracker.rey
  action:
    service: persistent_notification.create
    data_template:
      message:  >
        {{ trigger.to_state.attributes.friendly_name }} is {% if trigger.to_state.state == 'not_home' %}away{% else %}home{% endif %} since {{now().strftime("%H:%M:%S")}}
      notification_id: "occupants"
