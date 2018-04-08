# Quick Toggles on Android

## Requirements: 
- Tasker knowledge 
- AutoNotifcation

### Plugins:
AutoNotification can be found here: https://play.google.com/store/apps/details?id=com.joaomgcd.autonotification28
I recommend to buy the unlocked version, or to get a subscription to AutoApps (full pack, all unlocked + betas + alphas)

## Explanation:

First create a toggle on your quick settings, you can create 20 different toggles if you want...

First you need to understand how to use Tasker to control your devices on HASS by using HTTP post and JSON.

What I did to create toggles like this:
I prefer to create two task (because I can use those tasks in other tasks as well).
Example: Control Living Lights, so I create a task **HA - Living Top On** and **Living Top Off**

#### Step 1: Checking your global variables
Be sure before you start, that you have setup your tasker correctly, by creating global variables. This is explained here: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Setting_Global_Variables.md

#### Step 2: Check your tasks to control your devices
In previous tutorials, was explained how to create seperate tasks to control your devices in Tasker. Be sure that you have created such tasks. It is explained here: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Control_Hass_Devices.md

#### Step 3: Create a toggle
To do so, you need to create 5 actions. So the task will be like this:

- Action 1: If %Livinglights ~ On
- Action 2: Perform task: Living Lights OFF
- Action 3: Else if %Livinglights ~ Off
- Action 4: Perform task: Living Lights ON
- Action 5: End If

So now you have created your toggle task for your light.

#### Let's create another toggle to control other toggles as well, I call it eg: Toggle control
Inside that task, it contain the following actions:

- Action 1: Perform task: Toggle Living Lights if %ancomm ~ living (this is the same on the right side of the =:= of the command earlier)
- Action 2: if you have more toggles you can add here....

Now only 1 thing to do is create a profile to link the toggle task to it. That is by using AutoNotification

- Profile > Event > AutoNotification
- As message you type: Toggle

Link now your task Toggle control to it...

Summary: For each thing I created 2 task (because if I want I can use those task later on, in other tasks as well).
I created 1 toggle for the device. And I created 1 main task to control the commands of all my other toggles.

I also added some action, because I also can control it by KLWP if I want it, just by linking the right task to it...

If you use the Custom Quick Settings plugin, I would be similar, except, the 1st action in side your ON or OFF task would be replaced by the action of Custom Quick Toggles Settings...
