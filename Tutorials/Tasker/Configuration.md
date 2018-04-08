Home-Asistant: Configurate Tasker

Requirements:
An android phone
Tasker
Autovoice
Setup Tasker:

Step 1: Create your configuration task
First I like to setup several thing, so I made a task, that I only need to run once... I'm putting my host, password and my devices in here. (When a device changes, then I only need to change it on 1 place, and all the other tasks will change as well).

So a config task would be like this in tasker:
Variable set: %HASS_PSW To ?api_password=xxxxx
Variable set: %HASS_SERVICE to http://xxxx:8123/api/services/
Variable set: %HASS_STATE to http://xxxx:8123/api/states/
Add then your devices with your correct ID of HASS below eg:
Variable set: %HASS_WOL to switch.wol
Variable set: %HASS_TOPLIGHT to light.living_toplight
Variable set: %HASS_SIDELIGHT to light.living_sidelight
After creating this, you need to run this task, so Tasker knows all the variables and remember it.
