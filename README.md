
# Alfen Wallbox - HomeAssistant Integration

This is a custom component to allow control of Alfen Wallboxes in [HomeAssistant](https://home-assistant.io).

The component is a fork of the [Garo Wallbox custom integration](https://github.com/sockless-coding/garo_wallbox) and [egnerfl custom integration](https://github.com/egnerfl/alfen_wallbox)

> After reverse engineering the API myself I found out that there is already a Python libary wrapping the Alfen API.
> https://gitlab.com/LordGaav/alfen-eve/-/tree/develop/alfeneve
> 
> https://github.com/leeyuentuen/alfen_wallbox/wiki/API-paramID

## Installation

### Install using HACS (recommended)
If you do not have HACS installed yet visit https://hacs.xyz for installation instructions.

To add the this repository to HACS in your Home Assistant instance, use this My button:

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?repository=alfen_wallbox&owner=leeyuentuen&category=Integration)

After installation, please reboot and add Alfen Wallbox device to your Home Assistant instance, use this My button:

[![Open your Home Assistant instance and start setting up a new integration.](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=alfen_wallbox)

<details>

<summary><i><h2 style="display:inline-block">Manual configuration steps</h2></i></summary>

> In HACS, go to the Integrations section and add the custom repository via the 3 dot menu on the top right. Enter ```https://github.com/>> leeyuentuen/alfen_wallbox``` in the Repository field, choose the ```Integration``` category, then click add.\
> Hit the big + at the bottom right and search for **Alfen Wallbox**. Click it, then click the download button.\
>
> Clone or copy this repository and copy the folder 'custom_components/alfen_wallbox' into '<homeassistant config>/custom_components/alfen_wallbox'
>
> Once installed the Alfen Wallbox integration can be configured via the Home Assistant integration interface
where you can enter the IP address of the device.
>
</details>

### Home Assistant Energy Dashboard
The wallbox can be added to the Home Assistant Energy Dashboard using the `_meter_reading` sensor.

## Settings
The wallbox can be configured using the Integrations settings menu:

<img src="doc/screenshots/configure.png" alt="drawing" style="width:600px;"/>

Categories can be configured to refresh at each specified update interval. Categories that are not selected will only load when the integration starts. The exception to this rule is the `transactions` category, which will load only if explicitly selected.

To locate a category, start by selecting all categories. Allow the integration to load, then find the desired entity. The category will be displayed in the entity's attributes.

<img src="doc/screenshots/attribute category.png" alt="drawing" style="width:400px;"/>

Reducing the number of selected categories will enhance the integration's update speed.

## Services
Example of running in Services:
Note; The name of the configured charging point is "wallbox" in these examples.

### - Changing Green Share %
```
service: alfen_wallbox.set_green_share
data:
  entity_id: number.wallbox_solar_green_share
  value: 80
```

### - Changing Comfort Charging Power in Watt
```
service: alfen_wallbox.set_comfort_power
data:
  entity_id: number.wallbox_solar_comfort_level
  value: 1400
```

### - Enable phase switching
```
service: alfen_wallbox.enable_phase_switching
data:
  entity_id: switch.wallbox_enable_phase_switching
```


### - Disable phase switching
```
service: alfen_wallbox.disable_phase_switching
data:
  entity_id: switch.wallbox_enable_phase_switching
```

### - Enable RFID Authorization Mode
```
service: alfen_wallbox.enable_rfid_authorization_mode
data:
  entity_id: select.wallbox_authorization_mode
```

### - Disable RFID Authorization Mode
```
service: alfen_wallbox.disable_rfid_authorization_mode
data:
  entity_id: select.wallbox_authorization_mode
```

### - Reboot wallbox
```
service: alfen_wallbox.reboot_wallbox
data:
  entity_id: alfen_wallbox.garage
```

## Screenshots
<img src="doc/screenshots/wallbox-1.png"/>

![Wallbox 2](<doc/screenshots/wallbox-2.png>)

![Wallbox 3](<doc/screenshots/wallbox-3.png>)
