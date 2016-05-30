# stm32f030f4-adc-uart

This project uses STM32F030 controller to read temperature from LM335 and send it via UART. It also measures internal voltage reference (bandgap) with another channel of ADC to compute current voltage scale and then apply it to value got from temperature sensor:

            3300 * adc_temp * adc_int_ref
    Vadc = -------------------------------
                4096 * adc_int
    
- `adc_temp` - value from ADC-channel attached to external temperature sensor
- `adc_int` - value from ADC-channel attached to internal voltage reference
- `adc_int_ref` - factory "default" value for internal voltage reference, taken from system memory (for `3300` mV)

###Wiring

For TSSOP-20 package

- pin 16 (VDD) to +3.3
- pin 5  (VDDA) to +3.3
- pin 15 (GND) to GND
- pin 1  (BOOT0) to +3.3
- pin 4  (RESET) to GND, temporarily
- pin 8  (USART1_TX) to RX of the FTDI-cable
- pin 9  (USART1_RX) to TX of the FTDI-cable
- pin 6  (PA0) to LED
- pin 11 (PA5) to plus of LM335 (as ADC input)

LM335 has its minus on GND and its plus tied with 330 Ohm resistor to VDD (+3.3). External ceramic 1uF capacitor between VDD and GND seems to significantly improve ADC values stability.
