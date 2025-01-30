# izzymonitor
<a href="https://eigenlucy.github.io/projects/izzymonitor">esp32-s3 based home assistant control panel</a>

<a href="https://github.com/izzyhub/izzymonitor-firmware">firmware development repo</a>

# Downloading Gerbers/PCBA files for assembly service
PCBA files are generated in the build artifacts on each commit. Download the build artifacts from the latest commit under the Actions tab. Upload the default gerber zip to JLCPCB, and use default.csv for the BOM file + default.pos.csv for the CPL file

# Requirements 
<li><a href="https://docs.atopile.io/latest/">atopile</a></li>
<li><a href="https://rustup.rs/">rust</a>, <a href="https://docs.esp-rs.org/book/installation/riscv-and-xtensa.html">espup</a>, <a href="https://github.com/esp-rs/espflash">espflash</a></li>

# Directory
## Ato builds
<li>Ato builds listed in ato.yaml</li>
<li>Veramonitor.ato is the main build. The final PCB is build from this, and the corresponding kicad project is in elec/layouts/default/veramonitor.kicad_pro</li>
<li>kailh-sw.ato contains the keyswitch+neopixel module. kicad files are located in elec/layouts/kailh-sw</li>
<li>MAX98357AETE_plus_T.ato contains the ClassDAmp module</li>


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

Neopixel Pin Maping (veramonitor.ato, line 70):
```
    micro.io16 ~ sw1.DIN; sw1.DOUT ~ sw2.DIN; sw2.DOUT ~ sw3.DIN; sw3.DOUT ~ sw4.DIN; sw4.DOUT ~ sw5.DIN; sw5.DOUT ~ sw6.DIN
```
## <a href="https://jlcpcb.com/partdetail/Kailh-CPG1511F01S05/C400225">CPG1511F01S05</a> Kailh Switches
Accomodates standard keycaps
<a href="https://jlcpcb.com/parts/componentSearch?searchTxt=C400225">LCSC_ID: C400225</a> Kail module configured in elec/src/kailh-sw.ato.

Active low. Pin mappings:
```
    micro.io14 ~ sw1.KEY; micro.io21 ~ sw2.KEY; micro.io47 ~ sw3.KEY; micro.io48 ~ sw4.KEY; micro.io45 ~ sw5.KEY; micro.io35 ~ sw6.KEY
```

## <a href="https://www.digikey.com/en/products/detail/knowles/SPH0641LU4H-1/5332438">SPH0641LU4h1</a> MEMS microphone
<a href="https://jlcpcb.com/partdetail/Knowles-SPH0641LU4H1/C2879853">LCSC_ID = C2879853</a>

PDM Pin Mappings:
```
    pdm.pdm_sel ~ mic.SELECT; pdm.pdm_sel ~ micro.io3
    pdm.pdm_clk ~ mic.CLOCK; pdm.pdm_clk ~ micro.io5
    pdm.pdm_data ~ mic.DATA; pdm.pdm_data ~ micro.io4
```

# To Do 
## 1: Verify basic functionality
## 2: Finish rust firmware
## 3: Home assistant integration
## 4: 3D printed enclosure/wall panel mount
