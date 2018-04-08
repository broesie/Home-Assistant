# Themes in Home Asssistant

To include themes in Home Assistant, I prefer to do it this way

1. Create a folder "Templates"
2. Inside your configuration.yaml file be sure it is linked to your template files.

``` 
frontend:
  themes: !include templates/themes.yaml
``` 
