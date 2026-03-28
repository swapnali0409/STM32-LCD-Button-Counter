# STM32-LCD-Button-Counter
STM32 project where a push button is used to increment a counter and display numbers (0–9) on an LCD using GPIO in 8-bit mode.
# STM32 LCD Button Counter

## About this project
This project is a simple STM32 application where a push button is used to control a counter, and the value is displayed on an LCD.

Every time the button is pressed, the number increases and is shown on the LCD screen. After reaching 9, it resets back to 0.

I built this project to understand how GPIO input, LCD interfacing, and basic logic work together.

---

## What it does
- Reads button input (PC13)
- Increments a counter on each press
- Displays numbers (0 to 9) on LCD
- Resets counter after 9
- Uses LCD in 8-bit mode

---

## How it works (simple)
- Button is connected to PC13 (active LOW)
- When button is pressed → number increases
- LCD displays the updated number
- After 9 → counter resets to 0

**Flow:**
Button → Counter → LCD Display

---

## Logic used
```c
if(HAL_GPIO_ReadPin(GPIOC,GPIO_PIN_13)==GPIO_PIN_RESET)
{
    num++;

    if(num > 9)
        num = 0;

    while(HAL_GPIO_ReadPin(GPIOC,GPIO_PIN_13)==GPIO_PIN_RESET);
}

lcd_command(0x80);
lcd_data(num + '0');
```

## Pin Configuration
## Button
PC13 → Input (Push button)
Active LOW (pressed = 0)


## LCD Control Pins
RS → PB6
EN → PA6
RW → PA7 (kept LOW)
LCD Data Pins (8-bit)
D0 → PA10
D1 → PB3
D2 → PB5
D3 → PB4
D4 → PB10
D5 → PA8
D6 → PA9
D7 → PC7

## LCD Initialization
lcd_command(0x38); // 8-bit mode
lcd_command(0x0C); // display ON
lcd_command(0x06); // entry mode
lcd_command(0x01); // clear display


## Output
Press button → number increases
LCD shows values from 0 to 9
After 9 → resets to 0

## Why this project is useful

This project helped me understand:

GPIO input handling
LCD interfacing (8-bit mode)
Simple counter logic
Button debouncing


## Limitations
Uses polling (not interrupt-based)
No debounce delay (only blocking wait)
Limited to single digit (0–9)


## Future improvements
Use external interrupt for button
Add proper debounce logic
Display multi-digit numbers
Convert to 4-bit LCD mode (fewer pins)
Add UART debugging


## Final note

This project is a good step forward after basic LED control.

It combines input, output, and display — which is important for building real embedded systems.
