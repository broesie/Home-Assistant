# Create Notification with tasker based on Home Assistant devices.
This tutorial will learn you how to create notifications on your phone by using Tasker based on Home Assistant devices.

## Requirements:
- An android phone
- Tasker
- Join (You can find it here: https://play.google.com/store/apps/details?id=com.joaomgcd.join)
- Autonotification (option) (You can find it here: https://play.google.com/store/apps/details?id=com.joaomgcd.autonotification)

### Step 1: Configure Join in Home Assistant
- Configure your hass with Join (See: https://www.home-assistant.io/components/joaoapps_join/)

### Step 2: Create automations
Now it time to create some automations, examples are like this:

``` 
- id: notify_toplights_on
  alias: Alert - Toplights On
  trigger:
  - platform: state
    entity_id: light.living_toplights_level
    from: "off"
    to: "on"
  action:
  - service: joaoapps_join.nexus6p_send_tasker
    data:
      command: setvar=:=LivingLampTop=:=On
```
