# Create Home Assistant notifications with Tasker

This tutorial will explain how you can receive notifications on your android phone.

## Requirements:
- An android phone
- Tasker
- Join app (find it here: https://play.google.com/store/apps/details?id=com.joaomgcd.join)

### Step 1:
- Enable Join inside your Home Assistant Configuration: (See installation: https://www.home-assistant.io/components/joaoapps_join/)

### Step 2:
The're 2 ways to retrieve information from Home Assistant to your Tasker. You can use HTTP GET or you can use the AutoTools plugin.
Personal I prefer tot use AutoTools, because the programming is cleaner, and you don’t have to use split variables. You can realize it with only 1 action. If you don’t want to use a plugin, you still can realize is with HTTP GET…
I will explain both methods:

#### Method 1: Using HTTP GET
- Do a HTTP GET: as port: yourhost/api/states/yourentity?api_password=xxxx
In my case I use global variables, so I have it configure it 1 time in my programming. (see also how to configure Tasker for Home Assistant: https://github.com/broesie/Home-Assistant/blob/master/Tutorials/Tasker/Configuration.md).
So mine will be: %HASS_STATE%HASS_TOPLICHT%HASS_PSW
- Do a variable set *%source* to %HTTPD
Now you have to split the variables… If you don’t know what variables are, and what you can do, check my tutorial about variables: https://www.youtube.com/watch?v=F2IJJlUGF9E
- Do a variable split: %source splitter “state”
- Do a variable split: %source2 splitter "

your result will be in %source21 (you can use a flash, to check it)
Then you can an if statement if you want…
