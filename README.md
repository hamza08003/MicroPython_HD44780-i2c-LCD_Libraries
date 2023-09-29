## HD44780 Character LCD Micro-Python Libraries

This repository contains MicroPython libraries providing an API for interfacing with HD44780 compatible character LCDs. It includes two main components: `LcdApi`, a core library defining essential LCD commands and functions, and `I2cLcd`, an extension enabling I2C communication with HD44780 LCDs using PCF8574.

<br>

## ℹ️ Introduction

This README provides instructions on how to utilize the two Python libraries for interfacing with HD44780 compatible character LCDs. It walks you through the necessary steps to integrate these libraries into your project.

<br>

## ⚙️ Usage
### 1. Using `I2C` Class from Micro-Python `machine` library:

First of all, Import `I2C` class from `machine` library, then Create an instacne of the `I2C` class by passing *SDA* and *SCL* Pin Numbers along with their Bus Number 

```python
# I2C Constructor - General Syntax
i2c = I2C(id: int, scl: Pin, sda: Pin, freq: int = 400_000)
# Example
i2c = I2C(id=1, scl=Pin(3), sda=Pin(2))
```

<br>
   
### 2. Using `I2cLcd` Class from `machine_i2c_lcd` library:

Now, Import the `I2cLcd` class from the `machine_i2c_lcd` library and create an instance of it by passing the `I2C` instance we created in first step, the i2c address (usually it's *0x27*) and the number of rows & columns of LCD.

   ```python
   # I2cLcd Constructor - General Syntax
   lcd = I2cLcd(i2c: I2C, i2c_addr: int, num_lines: int, num_columns: int)
   # Example
   lcd = I2cLcd(i2c, 0x27, 2, 16)
   ```

<br>

### 3. Now you are ready to perform different operations on your LCD

   Try this basic example to display 'Hello World' on your LCD Screen

   ```python
   lcd.clear()
   lcd.show_cursor()
   lcd.blink_cursor_on()
   lcd.putstr("Hello\nWorld")
   ```
   
