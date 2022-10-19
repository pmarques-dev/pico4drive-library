# Pico4Drive Library

## Introduction

This library has functions to handle the peripherals on the Pico4Drive
development board. These include:
 - motor drivers
 - analog multiplexer
 - power monitoring and control

## Reference

### void pico4drive_init(void)

Initialize the library. This sets up the PWM timers, configure the ADC and  GPIO's to appropriate states.


### void pico4drive_set_motor_pwm(int driver, float value)

Set the motor PWM level for one driver.

Parameter|Description
---|---
driver|one of the DRV_1, ..., DRV_4 constants
value|pmw level from -1.0 to 1.0. Positive values will make the A output (positive) voltage higher than the B output


### uint16_t pico4drive_read_adc(int channel)

Read the analog value from one ofthe analog multiplexer input. Returns the ADC
value in the range 0 .. 4095

Parameter|Description
---|---
channel|channel number 0..7

### void pico4drive_poweroff(void)

Turns the board off. This can be used, for instance, to implement auto power off
after a period of inactivity.


### void pico4drive_update(void)

Update battery voltage and button state. The board updates this at roughly
50Hz, but this function can be called at a different rate. Calling it once
every 600ms is enough to not lose events (using the press count variable),
but it can be called at higher rates, e.g. 100Hz

The global variables updated after calling this function are:

Variable|Description
---|---
int battery_mV|board input voltage in mV
int on_button_state|current button state (1:pressed, 0:released)
uint32_t on_button_press_count|number of times the button has been pressed. If the update function is called unfrequently, looking at *on_button_state* may miss button press events, but this variable is always updated anyway
