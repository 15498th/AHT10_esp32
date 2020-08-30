## AHT10_esp32
Micropython library for AHT10 humidity and temperature sensor.
Heavily based on [https://github.com/Thinary/AHT10](https://github.com/Thinary/AHT10).

## Usage

```python
from machine import I2C
import aht10.py

# Create i2c bus object, pins here are hardware i2c pins for ESP32
i2c = I2C(0, sda=21, scl=22)

# Create sensor object. Default address argument is 56 and can be ommited
sensor = aht10.AHT10(i2c=i2c, address=56)

# Tell sensor to do a single measurement
sensor.initiateMeasurement()

# Wait for sensor to complete measurement. It takes about 75 ms according to manual
# Be aware that this might not be the best way to do it
time.sleep_ms(100)

# Read data from sensor memory to internal buffer
sensor.readRawData()

# Convert data from internal buffer to human readable format
temperature = sensor.convertTemperature()
humidity = sensor.convertHumidity()


# Reading property .values does all above combined
humidity, temperature = sensor.values
```

