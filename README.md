# esphome panel
esp32-s3 based home assistant control panel

# Requirements 
<li><a href="https://docs.atopile.io/latest/">atopile</a></li>
<li><a href="https://rustup.rs/">rust</a>, <a href="https://docs.esp-rs.org/book/installation/riscv-and-xtensa.html">espup</a>, <a href="https://github.com/esp-rs/espflash">espflash</a></li>

# TESTING IN PROGRESS:
## <a href="https://www.waveshare.com/wiki/1.8inch_LCD_Module">Wavshare 1.8in LCD Module</a> with <a href="https://crates.io/crates/st7735-lcd">ST7735 Controller</a>
module TFTDisplay in elec/src _1_peroid_8INCH_space_MODULE.ato
<a href="https://jlcpcb.com/partdetail/Waveshare-1_8inch_LCDModule/C359940">LCSC_ID = C359940</a>

SPI Pin mapping (elec/src/veramonitor.ato, line 67):
```
    lcd.spi.mosi ~ micro.io13; lcd.spi.sck ~ micro.io12; lcd.spi.cs ~ micro.io11; lcd.spi.dc ~ micro.io10; lcd.spi.reset ~ micro.io9; lcd.spi.backlightEN ~ micro.io46
```

##  <a href="https://learn.adafruit.com/adafruit-max98357-i2s-class-d-mono-amp/overview">MAX98357</a> Amp + Speaker  
Uses <a href="https://learn.adafruit.com/adafruit-max98357-i2s-class-d-mono-amp/overview">MAX98357</a> (LCSC ID = <a href="https://jlcpcb.com/partdetail/978950-MAX98357AETET/C910544">C910544</a>) 3W Class D amplifier IC + KLJ-1304T Speaker (LCSC_ID = C18186315). ESP32-S3 sends digital audio data to MAX98357 via I2S.

I2S Pin Mapping (veramonitor.ato, line 73):
```
    amp.LRCLK ~ micro.io8; amp.BCLK ~ micro.io18; amp.DIN ~ micro.io17
```
## Test <a href="https://jlcpcb.com/partdetail/OPSCOOptoelectronics-SK6805EC20/C2890036">SK6805 neopixels</a>
WS2812B style protocol. Defined in elec/src/sk6805-ec20/elec/src/sk6805-ec20.ato

Neopixels invoked and configured in each KailhSW module

Neopixel Pin Maping (veramonitor.ato, line 70)
```
    micro.io16 ~ sw1.DIN; sw1.DOUT ~ sw2.DIN; sw2.DOUT ~ sw3.DIN; sw3.DOUT ~ sw4.DIN; sw4.DOUT ~ sw5.DIN; sw5.DOUT ~ sw6.DIN
```
## Kailh Switches
Based on <a href="https://jlcpcb.com/partdetail/Kailh-CPG1511F01S05/C400225">CPG1511F01S05</a> <a href="https://jlcpcb.com/parts/componentSearch?searchTxt=C400225">LCSC_ID: C400225</a> Configured in elec/src/kailh-sw.ato. Each switch has a neopixel for backlighting.

Active low. Pin mappings:
```
    micro.io14 ~ sw1.KEY; micro.io21 ~ sw2.KEY; micro.io47 ~ sw3.KEY; micro.io48 ~ sw4.KEY; micro.io45 ~ sw5.KEY; micro.io35 ~ sw6.KEY
```

## Test microphone
SPH0641LU4H-1 MEMS Microphone (LCSC_ID = C2879853)

PDM Pin Mappings:
```
    pdm.pdm_sel ~ mic.SELECT; pdm.pdm_sel ~ micro.io3
    pdm.pdm_clk ~ mic.CLOCK; pdm.pdm_clk ~ micro.io5
    pdm.pdm_data ~ mic.DATA; pdm.pdm_data ~ micro.io4
```
## Test home assistant integration
    ESPHome Panel and/or Rust?
