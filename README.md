# Zorg

[![Join the chat at https://gitter.im/zorg-framework/zorg](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/zorg-framework/zorg?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Zorg is a Python framework for robotics and physical computing. It is based on
[Cylon.js][cylon.js], a JavaScript framework for robotics.

## Getting started

### Installation

All you need to get Zorg up and running is the `zorg` package:

```
pip install zorg
```

_You may need to [copy the source][zorg-source] if your device does not
support [pip][pip]._

You should also install the packages for the hardware you are looking to support. In our examples, we will be using the [Intel Edison][intel-edison] and an LED, so we need the `edison` and `gpio` packages:

```
pip install zorg-gpio zorg-edison
```

## Examples

### Intel Edison and an LED

This example controls an LED connected to the Intel Edison and blinks it once every 500 milliseconds. This program should be run on the Intel Edison itself.

```python
import zorg

def work (my):
    while True:
        # Toggle the LED
        my.led.toggle()

        # Wait 100ms before doing it again
        time.sleep(0.1)

robot = zorg.robot({
    "connections": {
        "edison": {
            "adaptor": "zorg_edison.Edison",
        },
    },
    "devices": {
        "led": {
            "connection": "edison",
            "driver": "zorg_gpio.Led",
            "pin": 13, # 13 is the on-board LED
        }
    },
    "name": "example", # Give your robot a unique name
    "work": work, # The method (on the main level) where the work will be done
})
```

[cylon.js]: https://github.com/hybridgroup/cylon/
[intel-edison]: https://www-ssl.intel.com/content/www/us/en/do-it-yourself/edison.html
[pip]: https://pip.pypa.io/en/stable/
[zorg-source]: https://github.com/gunthercox/zorg/archive/master.zip
