# Home-Asistant: Control it by voice by using Tasker (in any language)

This is a tutorial how you can control your devices by using your voice in your own language....
All this can be also triggered by Google Now.

## Requirements:
- An android phone
- Tasker
- Autovoice

## Setup Tasker:

### Step 1: Check your global variables

See the file configuration, how to setup the global variables. This is explained here: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Configuration.md

### Step 2: Check your Task to control your devices
In previous tutorials, was explained how to create seperate tasks to control your devices in Tasker.
Be sure that you have created such tasks. It is explained here: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Control_Hass_Devices.md

### Step 3: Configure your autovoice plugin:

- **Open de app: AutoVoice**
- **Activate Google Now integration**, if you want integration with Google Now
- Set your **language: General settings > Default Recognize Settings > Language Settings > Language (Also Language Code)**

**Don't forget to enable in your android settings, the accessibility for Autovoice**

### Step 4: Create your profile and task

#### Example 1: task to turn off/turn on task with if-else statements inside the task

##### Your profile:

- Create a **new profile**
  - Choose **Event > Plugin > Autovoice Recognize**
  - Choose **Advanced**
  - **Checkmark Regex**
  - As **command filter** use: **turn (?< state >.+) my (?< device >.+)** (Without any spaces between the < and > !)

##### Your task:

Work with if-else function

I prefer to use just the If statement instead of the if-else statement, because I can collapse my code...

#### Example 1: Turn Living Top Lights On or Off

- **If %state ~R on AND %device ~R living lights** (turn on living lights), use match regex!
  - **Perform Task: HA - LivingTop On** (See step 2)
- **End if**

- **If %state ~R off AND %device ~R living lights** (turn off living lights), use match regex!
  - **Perform Task: HA - LivingTop Off** (See step 2)
- **End if**

Also it can be shorter, if you want: just by using eg: **Perform Task: HA - LivingTop Off** and checkmark the if-statement, and put there: **If %state ~R off AND %device ~R living lights**. So in that case, you only use 1 action, instead of 3...

#### Example 2: Dim lights task

##### Your profile:

- Create a **new profile**
  - **Choose Event > Plugin > Autovoice Recognize**
  - **Choose Advanced**
  - **Checkmark Regex**
  - As **command filter** use: **dim (?< device >.+) to (?< percentage >.+)%** (Without any spaces between the < and > !)

##### Your task:

- **If %device ~R living lights ** (use match regex!)
  - **Variable set: %service** to **light/turn_on**
  - **HTTP Post:**
    - Service port: **%HASS_SERVICE%service%HASS_PSW**
    - In data / file: {"entity_id":"%HASS_TOPLIGHT","brightness":"%percentage"}
    - content/type: application/JSON
- **End if**

#### Other Commands

Above a little example to turn on or turn off things, but you can create also other profiles likes:

- **dim (?< device >.+) to (?< percentage >.+)%** (Without any spaces between the < and > !)
- **activate (?< scene >.+) mode** (Without any spaces between the < and > !)
- ....

The beauty of this, is that I can use Google now, so I can use Google AI to recognize my speech, and when I say a command by saying OK Google, it will also send it to my tasker autovoice...
