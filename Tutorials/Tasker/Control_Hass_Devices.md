# Control your Home Assistant devices from Tasker
In this tutorial, you will learn how to control your devices straight from Tasker.

## Requirements:
- An android phone
- Tasker

### Step 1: Check your global variables
Be sure before you start, that you have setup your tasker correctly, by creating global variables. This is explained here: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Configuration.md

### Step 2: Creating your tasks
I prefer to create a task for every state, eg: to power on my living lights, to power off my living lights, etc... The reason is very simple, that way I can call the task in other tasks as well, just by using **Perform Task**, so I don't have to configure it again.
That said, let's start:

- Create a **new task**, give it a name, **eg: HA - LivingTop On** (example: this will put my toplights in the living on)
- **Variable set: %service** to **light/turn_on**
- **HTTP Post:** 
  - Server:Port: **%HASS_SERVICE%service%HASS_PSW** (see step 1: global variables)
  - Data / File: **{"entity_id":"%HASS_TOPLICHT"}** (see step 1: global variables)
  - Content Type: **application/json**
  - **Enable Continue Task After Error**
  - Label: **Execute Service**
- **If %err is set** (I prefer to do a loop, if it gives a timeout...)
  - **Flash: Trying again** (just for letting you know, it will loop again, if timeouts)
  - **Go to action label Execute Service**
- **End if**

In this case I used a service: light/turn_on, but you can also use other services as well, like script/turn_on, etc... you can find that in the services of Home Assistant...
So you can create for everything another task, if you want... Then you can use the action **Perform Task**, whenever you want...
Example will be: when I use my voice command on my phone and say: Put the living toplights on, it will perform that task HA - LivngTop On.
Voice commands, more info in the tutorial about AutoVoice...
