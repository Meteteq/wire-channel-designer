# Contributing

Thanks for helping make Wire Channel Designer better. The most useful thing you can do is fix or add **pinouts**, because every board you add saves the next person a trip to the datasheet.

## Report a wrong or missing pinout (no coding)

In the tool, select the part, open **Props**, and tap **"Pinout wrong or missing? Report it"** (also in the 📌 Pinout reference). That opens a GitHub issue with the part's ID and current pins already filled in. Add the correct pins and a link to the datasheet or a photo of the silkscreen, and submit.

No account yet? Make a free one at github.com. It takes a minute.

## Fix it yourself (pull request)

The library is the `COMPONENT_LIBRARY` array near the top of `index.html`. Each part is one line:

```js
{"id":"mcu001","cat":"Microcontrollers","name":"ESP32 DevKit V1","sub":"30-Pin Standard, 30-pin, 28×51.5mm",
 "pkg":"DIP-30 Wide","w":28,"h":51.5,"d":13,"pins":30,"icon":"MCU","color":"#1a3a1a",
 "hd":2.5,"holes":[{"x":2.5,"y":2.5}, …],
 "pinout":[{"n":"3V3","x":1.3,"y":7.97,"s":"left"}, …],
 "v":"3.3V (5V USB)","proto":"WiFi/BLE/UART/SPI/I2C","awg":"24AWG / 26AWG","part":"ESP32-WROOM-32D"}
```

| Field | Meaning |
|---|---|
| `w`, `h`, `d` | Width, length and height in mm (`h` runs down the screen) |
| `holes` | Mounting holes, mm from the top-left corner; `hd` = hole diameter |
| `pinout[].n` | Pin name as printed on the board. Use `GND`, `3V3`, `5V`, `SDA`, `SCL`, `MOSI`, `MISO`, `SCK` where they apply, because the tool auto-connects those |
| `pinout[].x/y` | Pin position in mm from the top-left corner of the footprint |
| `pinout[].s` | Which side the pin label reads from: `left`, `right`, `top`, `bottom` |

Tips:
- Measure from the **top-left corner of the board outline**, with the USB port at the bottom, unless the board's usual orientation is obviously different.
- Header pins are 2.54 mm apart. If two rows are 25.4 mm apart, that's 10 × 2.54.
- Pin capabilities (ADC, input-only, boot pins) live in `pinInfo()` in `index.html`. If you add a new microcontroller family, add its rules there too.

Open a pull request with a link to your source in the description.

## Sharing parts without a pull request

**+ Add custom component** in the tool creates a part you can save with your layout. Paste its JSON into a "Request or add a component" issue and we'll merge it in.

## Bugs and ideas

Open an issue with what you did, what you expected, and a screenshot or the layout `.json` if you can.
