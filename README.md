## HD44780 Compatible Character Based LCD Micro-Python Libraries

This repository contains MicroPython libraries providing an API for interfacing with HD44780 compatible character LCDs. It includes two main components: `LcdApi`, a core library defining essential LCD commands and functions, and `I2cLcd`, an extension enabling I2C communication with HD44780 LCDs using PCF8574.

<br>

## ℹ️ Introduction

This README provides instructions on how to utilize the two Python libraries for interfacing with HD44780 compatible character LCDs. It walks you through the necessary steps to integrate these libraries into your project.

Before moving on to the Usage part, make sure to download both the `lcd_api.py` & `machine_i2c_lcd.py`. After downloading, place both the files in the same directory and create a new `main.py` file in the same directory, and here you will be writing all of your code discussed in the Usage Section. 

<br>

## ⚙️ Usage
### 1. Using `I2C` Class from Micro-Python `machine` library:

First of all, Import `I2C` class from `machine` library, then Create an instacne of the `I2C` class by passing *SDA* and *SCL* Pin Numbers along with their Bus Number, connected to LCD through I2C *PCF8574* module.

```python
from machine import I2C, Pin
# I2C Constructor
i2c = I2C(id: int, scl: Pin, sda: Pin, freq: int = 400_000)
# Example
i2c = I2C(id=1, scl=Pin(3), sda=Pin(2))
```

<br>
   
### 2. Using `I2cLcd` Class from `machine_i2c_lcd` library:

Now, Import the `I2cLcd` class from the `machine_i2c_lcd` library and create an instance of it by passing the `I2C` instance we created in first step and the number of rows & columns of LCD.

The i2c address is usually *0x27*, if *0x27* don't work try *0x3F* or you can check it for your own hardware through this code. This code will give you i2c address in HEX Format which you can then pass to the I2cLcd Constructor.

```python
from machine import I2C, Pin
i2c = I2C(id=1, scl=Pin(3), sda=Pin(2))
i2c_hex_scan = hex(i2c.scan()[0])
print(i2c_hex_scan)
```

   ```python
   from machine_i2c_lcd import I2cLcd
   # I2cLcd Constructor
   lcd = I2cLcd(i2c: I2C, i2c_addr: int, num_lines: int, num_columns: int)
   # Example
   lcd = I2cLcd(i2c, 0x27, 2, 16)
   ```

<br>

### 3. Now you are ready to perform different operations on your LCD

   Try this basic example to display numbers count on your LCD Screen

   ```python
   from machine import I2C, Pin
   from machine_i2c_lcd import I2cLcd
   
   i2c = I2C(1, sda=Pin(2), scl=Pin(3), freq=400000)
   lcd = I2cLcd(i2c, 0x27, 2, 16)
   
   def count_and_display(lcd, count):
      lcd.putstr("Let's Count:\n0-{}!".format(count))
      sleep(1.5)
      lcd.clear()
       
      for i in range(count + 1):
         lcd.putstr(str(i))
         sleep(0.75)
         lcd.clear()

   # Usage example
   count = 10  # Set the count to 10 or any desired count
   count_and_display(lcd, count)
   ```
For further opeerations which you can perform on your LCD, you can refer to the `lcd_api.py` and see all the availible methods there.
   
## 📋 Credits

This project includes code from the following sources:

- [Original Repository](https://github.com/dhylands/python_lcd) by [Dave Hylands](https://github.com/dhylands)
