# Quick Toggles on Android

## Requirements: 
- Tasker knowledge 
- AutoNotifcation

### Plugins:
AutoNotification can be found here: https://play.google.com/store/apps/details?id=com.joaomgcd.autonotification28
I recommend to buy the unlocked version, or to get a subscription to AutoApps (full pack, all unlocked + betas + alphas)

### Step 1: Checking your global variables
Be sure before you start, that you have setup your tasker correctly, by creating global variables. This is explained here: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Setting_Global_Variables.md

### Step 2: Check your tasks to control your devices
In previous tutorials, was explained how to create seperate tasks to control your devices in Tasker. Be sure that you have created such tasks. It is explained here: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Control_Hass_Devices.md

Example task of **HA - LivingTop On** will contain:

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
- **Variable set: %LivingTop** to **On**

### Step 3: Create a toggle task
You can do it with an if-else statement...
Let's assume you already created a task called **HA - LivingTop On** and **HA - LivingTop Off** in step 2.
So our toggle will be:

- **Create a task** called **Toggle - LivingTop ON/OFF**
- **If %LivingTop ~ On**
  - **Perform task: HA - LivingTop Off**
- **Else if %LivingTop ~ Off**
  - **Perform task: HA - LivingTop On**
- **End If**

So now you have created your toggle task for your toplight.

### Step 4: Put a quick toggle in your notificationbar
Open your notificationbar, click on the gear icon, then you can change your notification icons. When you scroll down, you can add a Autonotification Toggle. Put a Autonotification toggle in your notificationbar. **Be sure, you remember which one! All the notification icons are numbered, so remember the number!!** Let's assume we add the AutoNotification 2 inside the Notificationbar.

### Step 5: Edit your task to turn on and turn off your light
Now we have to edit the task **HA - LivingTop Off** and **HA - LivingTop On**, because we will link it with the toggle of step 4.
For example we edit the task **HA - LivingTop On**. At the end of the task, we add 1 action:

- **Autonotifcation Tiles:** 
  - **Tile 2**
  - Icon: **choose an icon**
  - Status icon: **choose an icon**
  - Label: **Living Top**
  - State: **Active**
  - Command: **Toggle=:=livingtop**

Now you can do the same for the task **HA - LivingTop Off**, but change the **state** to **Inactive**.

### Step 6: Create a command filter to receive the commands given based on the toggles
As you see in step 5, it will send a command, so we will create something that will react on it.

- **Create a new profile**, called **Toggle - Control Commands** (Profile > Event > AutoApps)
- **AutoApps command**
  - **Command filter: Toggle=:=**
- **Create a new task**, called **Toggle - Control Commands**
  - Inside that task it will be like:
    - **Perform task: Toggle - LivingTop ON/OFF** if **%aacomm ~ livingtop**
    - **Perform task: xxx** if **%aacomm ~ xxx**
    - **Etc..**

If **you don't have an AutoApps subscription** and you **use only AutoNotification**, the profile trigger will be **Profile > Event > AutoNotification** and inside the task it will be **%ancomm instead of %aacomm**
