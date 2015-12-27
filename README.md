# homebridge-rcswitch-gpiomem

<http://n8henrie.com/2015/12/control-an-rf-outlet-with-siri-via-homebridge>

Control RF outlets with HomeKit / Siri using
[rcswitch-gpiomem](https://github.com/n8henrie/node-rcswitch-gpiomem)

# Installation

1. Install [WiringPi](https://projects.drogon.net/raspberry-pi/wiringpi/download-and-install/)
1. Install homebridge: `npm install -g homebridge`
1. Install homebridge-rcswitch-gpiomem: `npm install --global
   homebridge-rcswitch-gpiomem`
1. Update your configuration file.

# Configuration

See `sample-config.json`

Either `onCode` and `offCode` **or** `systemcode` and `unitcode` are required.
My switches use on and off codes, so that's what I recommend and all I can
really help with.

- `accessory`: Must be `RCSwitch` (case sensitive)
- `name` :: string :: What you want to call the switch. Keep in mind
  that Siri will prefer anything other than your homebridge switch if there's
  any confusion, so name it something unique
- `onCode`, `offCode` :: int or string
    - If int: Decimal RF code to turn switch on / off
    - If string: Binary RF code to turn switch on / off
- `systemcode` :: string :: RF system code. I don't use this, please
  refer to other docs.
- `unitcode` ::  int :: RF unit code. I don't use this, please refer
  to other docs.
- `pin` :: int, optional :: BCM pin connected to 433 mhz transmitter, defaults
  to `17`
- `pulseLength` :: int, optional :: RF pulse length, defaults to `190`
- `bitLength` :: int, optional :: bit length of RF code, only used if using
  decimal RF code, defaults to `24`
