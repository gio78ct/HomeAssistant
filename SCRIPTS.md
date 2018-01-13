Se in uno script c'è nella sequenza un "delay", allora nell'interfaccia lo script vine rappresentato come uno switch invece che con il tasto "activate" accanto.
Si risolve aggiungendo in customize.yaml, in corrispondenza dello script, la voce "can_cancel: false" (opportunamente indentata) https://community.home-assistant.io/t/run-automation-with-button-to-click/23955/2 
