# DHT11 Python library

Originally forked from https://github.com/szazo/DHT11_Python
He did not use the huge Adafruit library.

I changed the pin and documented the pin better.

This simple class can be used for reading temperature and humidity values from DHT11 sensor on Raspberry Pi.

# Connect

[![badge](https://raw.githubusercontent.com/gejanssen/dht11_python/master/rpi-dht11.jpg)](https://raw.githubusercontent.com/gejanssen/dht11_python/master/rpi-dht11.jpg)

# Usage

1. Instantiate the `DHT11` class with the pin number as constructor parameter.
2. Call `read()` method, which will return `DHT11Result` object with actual values and error code.

For example:

```python
import RPi.GPIO as GPIO
import dht11

# initialize GPIO
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)
GPIO.cleanup()

# read data using pin 6 / bcm17
instance = dht11.DHT11(pin=17)
result = instance.read()

if result.is_valid():
    print("Temperature: %-3.1f C" % result.temperature)
    print("Humidity: %-3.1f %%" % result.humidity)
else:
    print("Error: %d" % result.error_code)
```

For working example, see `dht11_example.py` (you probably need to adjust pin for your configuration)
The file dht11.py is the library and does not need to be edited.


# License

This project is licensed under the terms of the MIT license.
