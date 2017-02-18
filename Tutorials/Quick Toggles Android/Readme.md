# Quick Toggles on Android

## Requirements: 
- Tasker knowledge 
- AutoNotifcation or Custom Quick Settings...

First of all, you can do it by using 2 different plugins.
For people who knows me, they know I'm a big fan of the Autoapps. (you can see that in the tutorials I made on youtube, (made more then 100 tutorials for tasker)
I prefer to use the autoapps, because that bundle can do way more things, that you possible can think.
Autoapps contains AutoNotification, AutoVoice, AutoContacts, AutoRemote, AutoArduino, AutoShare, and way more...
In my case I use AutoNotification to control my Quick Toggles...
It can be used without root. Also my phone is running Android Nougat 7.0 (Nexus 6P)
AutoNotification can be found here: https://play.google.com/store/apps/details?id=com.joaomgcd.autonotification28
I recommend to buy the unlocked version, or to get a subscription to AutoApps (full pack, all unlocked + betas + alphas)

Another way is using Custom Quick Settings. That can be also used for lower versions of android.
I dont prefer this method, because it has way less possibilities...
Custom Quick Settings can be found here; https://play.google.com/store/apps/details?id=com.quinny898.app.customquicksettings26

I will explain the method of AutoNotification:
First create a toggle on your quick settings, you can create 20 different toggles if you want...

First you need to understand how to use Tasker to control your devices on HASS by using HTTP post and JSON.
You can find info on this post: https://community.home-assistant.io/t/create-your-own-personal-assistent-with-tasker-in-multi-language-google-now-integration/3147

What I did to create toggles like this:
I prefer to create two task (because I can use those tasks in other tasks as well).
Example: Control Living Lights, so I create a task 'Living Lights ON' and 'Living Lights OFF'
Also for example I use the 2nd AutoNotifcation Toggle.

So my task for Living Lights ON would be like this:

- Action 1: AutoNotification Tiles: Tile 2, Command: Toggle=:=living, Icon: Icon choosen from the iconpack, State: Active, Label; Living Lights
- Action 2: HTTP Post: http://yourhost:8123/api/services/light/turn_on?api_password=xxxxx
inside DATA / File: {"entity_id":"your id of your device"}
content type: application/json
- Action 3: Set variable: %Livinglights to On
For the Living Lights OFF you do the same, but in action 1, you set as state Inactive, and in action two, you use light/turn_off, and action 3 would be Set variable %Livinglights to Off

So those 2 tasks can put your lights either on or off...

So let's create now a toggle task. I call it for example: 'Toggle Living Lights'
To do so, you need to create 5 actions. So the task will be like this:

Action 1: If %Livinglights ~ On
Action 2: Perform task: Living Lights OFF
Action 3: Else if %Livinglights ~ Off
Action 4: Perform task: Living Lights ON
Action 5: End If
So now you have created your toggle task for your light.

Let's create another toggle to control other toggles as well, I call it eg: Toggle control
Inside that task, it contain the following actions:

Action 1: Perform task: Toggle Living Lights if %ancomm ~ living (this is the same on the right side of the =:= of the command earlier)
Action 2: if you have more toggles you can add here....
Now only 1 thing to do is create a profile to link the toggle task to it. That is by using AutoNotification

Profile > Event > AutoNotification
As message you type: Toggle
Link now your task Toggle control to it...

Summary: For each thing I created 2 task (because if I want I can use those task later on, in other tasks as well).
I created 1 toggle for the device. And I created 1 main task to control the commands of all my other toggles.

I also added some action, because I also can control it by KLWP if I want it, just by linking the right task to it...

If you use the Custom Quick Settings plugin, I would be similar, except, the 1st action in side your ON or OFF task would be replaced by the action of Custom Quick Toggles Settings...
