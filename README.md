Mycroft
==========

Full docs at: https://docs.mycroft.ai

Pair Mycroft instance with Cerberus Account Management Service: https://cerberus.mycroft.ai

# Getting Started in Ubuntu - Development Environment
- Install ` virtualenv` >= 13.1.2 and `virtualenvwrapper` (Restart session)
- Install the following native packages
  - `libtool`
  - `autoconf`
  - `bison`
  - `swig`
  - `libglib2.0-dev`
  - `portaudio19-dev`
  - `python-dev`
  - `curl`
  - `mpg123`
  - `espeak`

# In addition, if you are running Ubuntu 16.04 or another O/S
- Install:
  - `libffi-dev`
  - `libssl-dev` 

- run `dev_setup.sh` (feel free to read it, as well)
- Restart session (reboot computer, or logging out and back in might work).

## Cerberus Device and Account Manager
Mycroft AI, Inc. - the company behind Mycroft maintains the Cerberus device and account management system. Developers can sign up at https://cerberus.mycroft.ai

By default the Mycroft software is configured to use Cerberus, upon any request such as "Hey Mycroft, what is the weather?", you will be informed that you need to pair and Mycroft will speak a 6-digit code, which you enter into the pairing page on the [Cerberus site](https://cerberus.mycroft.ai).

Once signed and a device is paired, the unit will use our API keys for services, such as the STT (Speech-to-Text) API. It also uses allows you to use our API keys for weather, Wolfram-Alpha, and various other skills.

Pairing information generated by registering with Cerberus is stored in:

`~./mycroft/identity/identity.json` <b><-- DO NOT SHARE THIS WITH OTHERS!</b>

It's useful to know the location of the identity file when troubleshooting device pairing issues.

## Using Mycroft without Cerberus.
If you do not wish to use our service, you may insert your own API keys into the configuration files listed below in <b>configuraion</b>.

The place to insert the API key looks like the following:

`[WeatherSkill]`

`api_key = ""`

Put the relevant key in between the quotes and Mycroft Core should begin to use the key immediately.

### API Key services

- [STT API, Google STT](http://www.chromium.org/developers/how-tos/api-keys)
- [Weather Skill API, OpenWeatherMap](http://openweathermap.org/api)
- [Wolfram-Alpha Skill](http://products.wolframalpha.com/api/)

These are the keys currently in use in Mycroft Core.

## Configuration
Mycroft configuration consists of 3 possible config files.
- `defaults.ini`, which lives inside the mycroft codebase/distribution
- `/etc/mycroft/mycroft.ini`
- `$HOME/.mycroft/mycroft.ini`

When the configuration loader starts, it looks in those locations in that order, and loads ALL configuration. Keys that exist in multiple config files will be overridden by the last file to contain that config value. This results in a minimal amount of config being written for a specific device/user, without modifying the distribution files.

## Starting the Virtualenv
To ensure that you are in the Mycroft virtualenv before trying to start the services, as everything is installed there, Run:
```
workon mycroft
```

### Running the initial stack
- run `PYTHONPATH=. python client/speech/main.py` # the main speech detection loop, which prints events to stdout and broadcasts them to a message bus
- run `PYTHONPATH=. python client/messagebus/service/main.py` # the main message bus, implemented via web sockets
- run `PYTHONPATH=. python client/skills/main.py` # main skills executable, loads all skills under skills dir

### Running stack via the script
- run `./start.sh service`
- run `./start.sh skills`
- run `./start.sh voice`
