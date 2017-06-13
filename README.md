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
- `repeats` :: int, optional :: Number of times to repeat the transmission of
  the code, defaults to 10 (as per [the original rcswitch
  code](https://github.com/sui77/rc-switch/blob/a7333b87d7e3ef8d9ce2eb6ca44843a8d19e7393/RCSwitch.cpp#L103))

# FAQ / Troubleshooting

It seems that the `gpiomem` system I use and the SysFS method of interacting with the GPIO are not compatible for reasons [explained in this issue](https://github.com/n8henrie/homebridge-rcswitch-gpiomem/issues/11). Make sure that you aren't also using programs that access the GPIO by way of SysFS or this library may not work.

# Changelog

## 20160727 :: 1.1.3

- Move `setRepeatTransmit` to just before calling `switchOn()` to facilitate
  multiple switches with different desired repeat counts

## 20160727 :: 1.1.2

- Move `setPulseLength` from initialization to just before calling `switchOn()`
  to facilitate multiple switches with different pulse lengths (closes #2).
