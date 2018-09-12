# USB Midi

You can use any generic midi device to remote control the mixer via mixing station.

## Requirements
**Note:** MCU or HUI modes are not supported!

### Android
- [USB OTG](http://en.wikipedia.org/wiki/USB_On-The-Go) compatible Android device
- [USB OTG cable](https://www.google.com/search?q=USB+OTG+cable) / USB host port
- Mixing Station Pro

#### Known issues
In Android 5.0 (Lollipop) only the last plugged USB device is working correctly. This is a [known bug](https://code.google.com/p/android/issues/detail?id=159897) in Android and cannot be fixed.

### iOS
- Not supported yet


## Overview
A midi device will be represented in the app as one or more input / output devices.
In the app you define `faders`, `buttons` and `knobs` which then use one of those input/output devices.

- Midi controller (fader, button, ..)
	- Use one midi input and output device assigned
	- Have one or more actions assigned which define what should be controlled

Make sure you're selecting the correct controller type:

- Button: Midi device sends a value when pressed and/or released
- Fader: Midi device sends an absolute value when fader/knob is moved (e.g. `0-127`)
- Knob: Midi device sends a fixed value for each increment / decrement (e.g. `24` and `27`)

## Midi Setup
The midi overview can be opened from the mixer via the menu:
```
Menu -> Setup -> Midi
```
You can add / edit midi controllers from here.

### Add a new controller
1. Press the `+` item in the menu to add a new controller.
2. Select the controller

### Configure a controller
The edit controller view allows you to change the properties of the controller:

- Unique name: Name which will be shown in the controller overview
- Input/Output: Selects which USB device should be used for Midi communication

#### Output Modes
The output mode configures when the value should be send back to the midi device.

| Mode | Description |
| -- | -- |
| On value change | Sends midi value when the action value has been changed without a midi input |
| On midi event+change | Sends a midi event when a midi event was received or the action value has been changed |
| On note up+change | Sends a midi event when a "note up" command was received or the action value has been changed |

#### Mapping a midi parameter
In general you can just press the `Learn` button and move/press the fader/button you want to assign.
The app will automatically detect the midi channel and parameter type.

You can also configure the parameters yourself:

- Event type: The event type defines what midi command the controller should react to

	| Event type | Description |
	| -- | -- | 
	| Note On/Off | Triggers the action on "Note On" and "Note Off" events |
	| Note On Triggers the actions on "Note On" events |
	| Note Off | Triggers the actions on "Note Off" events |
	| CC | Triggers the actions on "Control Change" events |
	| Pitch | Triggers the actions on "Pitch" events |

- Channel: The midi channel which should be used
- Param A/B: These two selections are for filtering the midi parameter.
Depending on the current selected event type the names of the parameters will change.
A value of `-1` means that the value will be ignored.
- Value source: Selects which midi parameter should be used as a value source.
Example: A fader sends midi CC events. The position of the fader will be sends as `Value` of the CC command so this parameter should be used. Select `Param B` to select the second parameter which is in this case
the `Value` parameter.

	Note: Buttons do not require a value source because the action will be triggered as soon as a matching midi command was received.

#### Additional button settings
- Output "on" value: Sets the value that should be send when the button is currently `on`. Some midi devices can show different colors depending on the midi value so this parameter can be used to change the color.
- Mode: How the button should react to midi commands

	| Mode | Description |
	| -- | -- |
	| Toggle | One button press toggles the value |
	| Momentary | Press and hold for a `on` command. Release for an `off` command |
	| Momentary inv. | Same as `Momentary` but inverted |

#### Additional rotary settings
- Multiplier: Sets the sensitivity of one increment/decrement step
- Inc value: Midi value for a single increment
- Dec value:  Midi value for a single decrement