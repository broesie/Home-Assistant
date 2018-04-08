# Home-Asistant: Control it by voice by using Tasker (in any language)

This is a tutorial how you can control your devices by using your voice in your own language....
All this can be also triggered by Google Now.

## Requirements:
- An android phone
- Tasker
- Autovoice

## Setup Tasker:

### Step 1: Create your configuration task

See the file configuration, how to setup the global variables.

### Step 2: Configure your autovoice plugin:

- **Open de app: AutoVoice**
- **Activate Google Now integration**, if you want integration with Google Now
- Set your **language: General settings > Default Recognize Settings > Language Settings > Language (Also Language Code)**

**Don't forget to enable in your android settings, the accessibility for Autovoice**

### Step 3: Create your profile and task

#### Example 1: task to turn off/turn on task with if-else statements inside the task

##### Your profile:

- Create a **new profile**
  - Choose **Event > Plugin > Autovoice Recognize**
  - Choose **Advanced**
  - **Checkmark Regex**
  - As **command filter** use: **(?< task >.+) my (?< device >.+)** (Without any spaces between the < and > !)

##### Your task:

Work with if-else function

I prefer to use just the If statement instead of the if-else statement, because I can collapse my code...

- **If %task ~ turn on AND %device ~ living lights** (turn on living lights)
- **Variable set: %service to light/turn_on**
- **HTTP Post:**
  - **Service port: %HASS_SERVICE%service%HASS_PSW**
  - **In data / file: {"entity_id":"%HASS_TOPLIGHT","brightness":"255"}**
  - **content/type: application/JSON**
- **End if**

- **If %task ~ turn off AND %device ~ living lights (turn off living lights)**
- **Variable set: %service** to **light/turn_off**
- **HTTP Post:**
  - **Service port: %HASS_SERVICE%service%HASS_PSW**
  - **In data / file: {"entity_id":"%HASS_TOPLIGHT"}**
  - **content/type: application/JSON**
- **End if**

...

#### Example 2: Dim lights task

##### Your profile:

- Create a **new profile**
  - **Choose Event > Plugin > Autovoice Recognize**
  - **Choose Advanced**
  - **Checkmark Regex**
  - As **command filter** use: **dim (?< device >.+) to (?< percentage >.+)%** (Without any spaces between the < and > !)

##### Your task:

- **If %device ~ living lights **
- **Variable set: %service** to **light/turn_on**
- **HTTP Post:**
 - S**ervice port: %HASS_SERVICE%service%HASS_PSW**
 - **In data / file: {"entity_id":"%HASS_TOPLIGHT","brightness":"%percentage"}**
 - **content/type: application/JSON**
- **End if**

#### Other Commands

Above a little example to turn on or turn off things, but you can create also other profiles likes:

- **dim (?< device >.+) to (?< percentage >.+)%** (Without any spaces between the < and > !)
- **activate (?< scene >.+) mode** (Without any spaces between the < and > !)
- ....

You only need to change data and attributes...

The beauty of this, is that I can use Google now, so I can use Google AI to recognize my speech, and when I say a command by saying OK Google, it will also send it to my tasker autovoice...
