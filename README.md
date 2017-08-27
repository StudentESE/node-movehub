# movehub

[![NPM version](https://badge.fury.io/js/movehub.svg)](http://badge.fury.io/js/movehub)
[![Dependency Status](https://gemnasium.com/badges/github.com/hobbyquaker/node-movehub.svg)](https://gemnasium.com/github.com/hobbyquaker/node-movehub)
[![Build Status](https://travis-ci.org/hobbyquaker/node-movehub.svg?branch=master)](https://travis-ci.org/hobbyquaker/node-movehub)
[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)
[![License][mit-badge]][mit-url]

> Node.js interface for the Lego Boost Move Hub

**WORK IN PROGRESS - UNFINISHED!**


## Install

```
$ npm install movehub
```


## TODO

- [x] LED control
- [x] Motor control
- [ ] Sound playback
- [x] Emit distance sensor events
- [x] Emit color sensor events
- [ ] Emit rotation events
- [ ] Emit tilt sensor events
- [ ] Emit changed rssi values
- [ ] Connect to multiple Move Hubs
- [x] Generate API Docs
- [ ] Command wrappers behaving like the command blocks in the app (specific for "Franky the Cat", "Vernie the Robot" 
etc)

## API

<a name="Boost"></a>

## Boost
**Kind**: global class  

* [Boost](#Boost)
    * [.disconnect()](#Boost+disconnect)
    * [.motorTime(port, seconds, [dutycyle], [callback])](#Boost+motorTime)
    * [.motorAngle(port, angle, [dutycyle], [callback])](#Boost+motorAngle)
    * [.led(color, [callback])](#Boost+led)
    * [.subscribe(port, [callback])](#Boost+subscribe)
    * [.unsubscribe(port, [callback])](#Boost+unsubscribe)
    * ["scanning"](#Boost+event_scanning)
    * ["hub-found"](#Boost+event_hub-found)
    * ["connect"](#Boost+event_connect)
    * ["color"](#Boost+event_color)
    * ["distance"](#Boost+event_distance)
    * ["port"](#Boost+event_port)
    * ["disconnect"](#Boost+event_disconnect)

<a name="Boost+disconnect"></a>

### boost.disconnect()
Disconnect from Move Hub

**Kind**: instance method of [<code>Boost</code>](#Boost)  
<a name="Boost+motorTime"></a>

### boost.motorTime(port, seconds, [dutycyle], [callback])
Run a motor for specific time

**Kind**: instance method of [<code>Boost</code>](#Boost)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| port | <code>string</code> \| <code>number</code> |  | possible string values: `A`, `B`, `AB`, `C`, `D` |
| seconds | <code>number</code> |  |  |
| [dutycyle] | <code>number</code> | <code>100</code> | motor power percentage from `-100` to `100`. If a negative value is given rotation is counterclockwise. |
| [callback] | <code>function</code> |  |  |

<a name="Boost+motorAngle"></a>

### boost.motorAngle(port, angle, [dutycyle], [callback])
Turn a motor to specific angle

**Kind**: instance method of [<code>Boost</code>](#Boost)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| port | <code>string</code> \| <code>number</code> |  | possible string values: `A`, `B`, `AB`, `C`, `D` |
| angle | <code>number</code> |  | degrees to turn from `0` to `4026531839` |
| [dutycyle] | <code>number</code> | <code>100</code> | motor power percentage from `-100` to `100`. If a negative value is given rotation is counterclockwise. |
| [callback] | <code>function</code> |  |  |

<a name="Boost+led"></a>

### boost.led(color, [callback])
Control the LED on the Move Hub

**Kind**: instance method of [<code>Boost</code>](#Boost)  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>boolean</code> \| <code>number</code> \| <code>string</code> | If set to boolean `false` the LED is switched off, if set to `true` the LED will be white. Possible string values: `off`, `pink`, `purple`, `blue`, `lightblue`, `cyan`, `green`, `yellow`, `orange`, `red`, `white` |
| [callback] | <code>function</code> |  |

<a name="Boost+subscribe"></a>

### boost.subscribe(port, [callback])
Subscribe for sensor notifications

**Kind**: instance method of [<code>Boost</code>](#Boost)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> \| <code>number</code> | e.g. call `.subscribe('C')` if you have your distance/color sensor on port C. |
| [callback] | <code>function</code> |  |

<a name="Boost+unsubscribe"></a>

### boost.unsubscribe(port, [callback])
Unsubscribe from sensor notifications

**Kind**: instance method of [<code>Boost</code>](#Boost)  

| Param | Type |
| --- | --- |
| port | <code>string</code> \| <code>number</code> | 
| [callback] | <code>function</code> | 

<a name="Boost+event_scanning"></a>

### "scanning"
reports `true`/`false` when noble starts/stops to scan for BLE devices

**Kind**: event emitted by [<code>Boost</code>](#Boost)  
<a name="Boost+event_hub-found"></a>

### "hub-found"
Fires when a Move Hub is found

**Kind**: event emitted by [<code>Boost</code>](#Boost)  
**Properties**

| Name | Type |
| --- | --- |
| uuid | <code>string</code> | 
| address | <code>string</code> | 
| localName | <code>string</code> | 
| rssi | <code>number</code> | 

<a name="Boost+event_connect"></a>

### "connect"
Fires when a connection to the Move Hub is established

**Kind**: event emitted by [<code>Boost</code>](#Boost)  
<a name="Boost+event_color"></a>

### "color"
Fires on color sensor changes (you have to subscribe the port of the
sensor to receive these events).

**Kind**: event emitted by [<code>Boost</code>](#Boost)  
<a name="Boost+event_distance"></a>

### "distance"
Fires on distance sensor changes (you have to subscribe the port of the
sensor to receive these events).

**Kind**: event emitted by [<code>Boost</code>](#Boost)  
<a name="Boost+event_port"></a>

### "port"
Fires on port changes

**Kind**: event emitted by [<code>Boost</code>](#Boost)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| port | <code>number</code> |  |
| state | <code>number</code> | action start: `0x01`, action finished: `0x0a`, conflict: `0x05` |

<a name="Boost+event_disconnect"></a>

### "disconnect"
**Kind**: event emitted by [<code>Boost</code>](#Boost)  


## Contributing

Pull Requests welcome! :-)


## Credits

Thanks to [Jorge Pereira](https://github.com/JorgePe) who analyzed and documented the move hub ble protocol:
https://github.com/JorgePe/BOOSTreveng


## Disclaimer

LEGO and BOOST are Trademarks from The LEGO Company, which does not support (most probably doesn't even know about) this 
project. And of course I'm not responsible for any damage on your LEGO BOOST devices - use it at your own risk.


## License

MIT (c) Sebastian Raff

[mit-badge]: https://img.shields.io/badge/License-MIT-blue.svg?style=flat
[mit-url]: LICENSE
