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


# Testrun

```
gej@rpi-zw3:~/DHT11_Python $ python3 dht11_example.py 
Traceback (most recent call last):
  File "dht11_example.py", line 17, in <module>
    result = instance.read()
  File "/home/gej/DHT11_Python/dht11.py", line 34, in read
    RPi.GPIO.setup(self.__pin, RPi.GPIO.OUT)
RuntimeError: No access to /dev/mem.  Try running as root!
gej@rpi-zw3:~/DHT11_Python $ 
```

Whoops, we need root rights

```
gej@rpi-zw3:~/DHT11_Python $ sudo python3 dht11_example.py 
Last valid input: 2020-02-26 20:05:02.934488
Temperature: 23.0 C
Humidity: 34.0 %
^CCleanup
gej@rpi-zw3:~/DHT11_Python $ 
```


# License

This project is licensed under the terms of the MIT license.
