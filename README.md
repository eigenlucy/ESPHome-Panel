# esphome panel
esp32-s3 based home assistant control panel

# TESTING IN PROGRESS:
## Checklist:

## Test LCD (SPI)
From esp32-s3/elec/src/esp32-s3.ato:
```
    lcd.spi.mosi ~ micro.io13; lcd.spi.sck ~ micro.io12; lcd.spi.cs ~ micro.io11; lcd.spi.dc ~ micro.io10; lcd.spi.reset ~ micro.io9; lcd.spi.backlightEN ~ micro.io46
```
## Test amplifier/speaker (I2S):
```
    amp.LRCLK ~ micro.io8; amp.BCLK ~ micro.io18; amp.DIN ~ micro.io17
```
## Test neopixels:
```
    micro.io16 ~ sw1.DIN; sw1.DOUT ~ sw2.DIN; sw2.DOUT ~ sw3.DIN; sw3.DOUT ~ sw4.DIN; sw4.DOUT ~ sw5.DIN; sw5.DOUT ~ sw6.DIN
```
## Test switches
```
    micro.io14 ~ sw1.KEY; micro.io21 ~ sw2.KEY; micro.io47 ~ sw3.KEY; micro.io48 ~ sw4.KEY; micro.io45 ~ sw5.KEY; micro.io35 ~ sw6.KEY
```

## Test microphone
```
    pdm.pdm_sel ~ mic.SELECT; pdm.pdm_sel ~ micro.io3
    pdm.pdm_clk ~ mic.CLOCK; pdm.pdm_clk ~ micro.io5
    pdm.pdm_data ~ mic.DATA; pdm.pdm_data ~ micro.io4
```
## Test home assistant integration
    ESPHome Panel and/or Rust?
