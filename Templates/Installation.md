# Themes in Home Asssistant

To include themes in Home Assistant, I prefer to do it this way

1. Create a folder "Templates"
2. Inside your configuration.yaml file be sure it is linked to your template files.

``` 
frontend:
  themes: !include templates/themes.yaml
``` 

### Change theme by using the frontend
If you want to change your theme directly from the frontend, then you have to create a script, input select. Also you have to edit your groups.

**Script:**
``` 
set_currenttheme:
  alias: 'Activeer current theme'
  sequence:
    - service: frontend.set_theme
      data_template:
        name: '{{states.input_select.current_theme.state}}'
``` 

**Input select:**
``` 
  current_theme:
    name: 'currenttheme'
    options:
     - 'darkcyan'
     - 'darkred'
     - 'midnight'
    initial: 'darkred'
    icon: 'mdi:palette'
``` 

**Groups:**
``` 
themes:
  name: My themes
  entities:
  - script.set_currenttheme
  - input_select.current_theme
``` 
