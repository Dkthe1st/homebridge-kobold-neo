# homebridge-kobold

This is a plugin for [homebridge](https://github.com/nfarina/homebridge) to control your [Vorwerk Kobold](https://www.vorwerk.de/) vacuum robot. You can download it via [npm](https://www.npmjs.com/package/homebridge-kobold).

It is based on naofireblade's `homebridge-neato` and nicoh88's `homebridge-vorwerk`.

## Features

- House Cleaning
  - Eco mode
  - Extra care navigation
  - Nogo lines
- Zone cleaning <sup>[1](#d7)</sup><sup>, </sup><sup>[2](#change-room)</sup>
- Spot cleaning
  - Individual spot size <sup>[1](#d7)</sup><sup>, </sup><sup>[3](#eve)</sup>
  - Clean twice <sup>[3](#eve)</sup>
- Return to dock
- Find the robot
- Schedule (de)activation
- Robot information
  - Battery level
  - Charging state
  - Dock occupancy
  - Model and firmware version
- Automatic or periodic refresh of robot state
- Multiple robots

> <b name="d7">1</b> Only available on the Neato D7.  

> <b name="change-room">2</b> You can send the robot from one room to another as well. He will return to the base, wait there some seconds and then starts cleaning the next room.

> <b name="eve">3</b> You need a third party app like eve to access these features.



## Installation

1. Install homebridge using: `npm install -g homebridge`
2. Install this plugin using: `npm install -g homebridge-kobold`
3. If you don't have a Neato account yet, create one [here](https://www.neatorobotics.com/create-account/).
4. Update your configuration file. See the sample below.

## Configuration

Add the following information to your config file. Change the values for email and password.

### Simple

```json
"platforms": [
	{
		"platform": "NeatoVacuumRobot",
		"email": "YourEmail",
		"password": "YourPassword"
	}
]
```

### Advanced

Below are explanations for advanced parameters to adjust the plugin to your needs. All parameters are *optional*.

**refresh**  
Timer for periodic refresh of robot state. The default is `auto`. The options are:  
`auto` Updates the robot state when a cleaning was started via homekit so that you can activate automations based on a successful cleaning.  
`120` Or any other time in seconds (minimum `60`) is required if you want to receive robot state updates after starting the cleaning from outside of homekit (e.g. neato app or schedule).  
`0` Disables background updates completely.

**hidden**  
List of plugin features that you don't want to use in homekit (e.g. `dock`, `dockstate`, `eco`, `nogolines`, `extracare`, `schedule`, `find`, `spot`).

```json
"platforms": [
	{
		"platform": "NeatoVacuumRobot",
		"email": "YourEmail",
		"password": "YourPassword",
		"refresh": "120",
		"hidden": ["dock", "dockstate", "eco", "nogolines", "extracare", "schedule", "find", "spot"]
	}
]
```

## Tested robots

- Vorwerk Kobold V300 

## Contributors
Many thanks go to
- [ghulands](https://github.com/ghulands) for finding and fixing a bug when no robot is associated with the neato account
- [Berkay](https://github.com/btutal) for adding the schema file to use the plugin with homebridge-config-ui-x
- [Antoine de Maleprade](https://github.com/az0uz) for adding the zone cleaning feature
- [DJay](https://github.com/DJay-X) for testing out tons of new beta versions
