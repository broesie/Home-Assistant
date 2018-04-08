# Create Notification with tasker based on Home Assistant devices.
This tutorial will learn you how to create notifications on your phone by using Tasker based on Home Assistant devices.

## Requirements:
- An android phone
- Tasker
- Join (You can find it here: https://play.google.com/store/apps/details?id=com.joaomgcd.join)
- Autonotification (option) (You can find it here: https://play.google.com/store/apps/details?id=com.joaomgcd.autonotification)

### Step 1: Configure Join in Home Assistant
- Configure your hass with Join (See: https://www.home-assistant.io/components/joaoapps_join/)

### Step 2: Create automations in Home Assistant
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

### Step 3: Let tasker react to incoming messages
As you see in the example of the previous step, hass will send a notification to my Nexus 6P, with a command setvar=:=LivingLampTop=:=On.
Now tasker has to do something when it receive something like that...
- **Create a profile**, give it a name, **eg: Join - Receive Vars**
  - Use as trigger / context: **Event > Plugin > Join**
  - As configuration: set **textfilter: setvar**
- **Create a new task**, give it a name, eg: **Join - Receive Vars**
  - **Variable set: %%joincomm(1)** to **%joincomm(2)** (setting global variables in tasker) (be sure that with joincomm1, you use 2 % signs!)
  - Then you can do what ever you want using if commands: eg: **Perform Task xxx** if **%joincomm(1) ~ LivingLampTop & joincomm(2) ~ On** (In perform task, you can enable the if statement) 
  
  In my case I have also several tasks, eg: HA - Alert Toplights On. This task will eg update my homescreen on my phone and also change my quick toggles on my phone.
  Example of the content of this task can be:
  - **Autonotification Tiles**, update tiles
  - **KLWP send variable** to update my homescreen
  - **Say: The toplights are on.**
  - etc...
  
