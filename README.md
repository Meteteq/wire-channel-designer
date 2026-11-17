# Wire Channel Board Designer

> A browser-based EDA-style tool for designing **3D-printable wire-channel circuit boards** — no install, no backend, runs entirely in one HTML file.

**Live tool:** https://meteteq.github.io/wire-channel-designer

---

## What is the 3DPCB Method?

The **3DPCB method** replaces traditional PCBs with 3D-printed PETG boards that have recessed wire-channel grooves machined into the surface. You:

1. Print the board in PETG (or similar)
2. Lay hookup wire into the channels
3. Solder component legs directly where they cross

No etching. No PCB fab. No soldermask. Just a printer, wire, and a soldering iron. Great for makers, accessibility device builders, one-offs, and rapid prototyping.

---

## Features

- **133-component library** — microcontrollers, SBCs, sensors, motors, power management, ICs, passives, connectors, and more
- **Drag-and-drop layout** — physical footprints with real mm dimensions
- **Automatic wire channel routing** — right-angle pathfinding between matched net names
- **Layer control** — route channels on top, bottom, or both sides
- **Wire gauge / channel sizing** — set channel width and depth per project
- **Net/signal labeling** — name nets (VCC, GND, SDA, SCL, etc.) and auto-color channels
- **DRC** — warns about off-board components, overlaps, edge violations
- **OpenSCAD export** — generates `.scad` with board body + channel cutouts
- **BOM export** — CSV with all placed components
- **Wiring legend export** — SVG of all nets and their colors
- **Community component library** — import/export JSON to share custom component definitions
- **Save/load** — full layout as JSON
- **Zero install** — single `.html` file, works offline

---

## Quick Start

1. Download `wire-channel-designer.html`
2. Open it in any modern browser
3. Set your board dimensions (top-left panel)
4. Drag components from the library onto the board
5. Assign net names to pins (click a pin → type net name)
6. Click **Auto-Route** to generate wire channels
7. Export OpenSCAD → open in OpenSCAD → render → export STL → slice → print

---

## Contributing Components

The component library lives in a single JavaScript array at the top of the HTML file:

```js
const COMPONENT_LIBRARY = [
  {
    id: 'esp32-devkit-v1',      // unique kebab-case ID
    cat: 'Microcontrollers',    // category (see list below)
    name: 'ESP32 DevKit V1',    // display name
    sub: '30-pin, 28×51.5mm',   // subtitle shown in picker
    w: 28.0,                    // physical width in mm
    h: 51.5,                    // physical height in mm
    pins: 30,                   // total pin count
    icon: 'MCU',                // 3-letter icon label
    color: '#1a3a1a',           // card background color
    holes: [                    // mounting hole positions (mm from top-left)
      {x: 3.5, y: 3.5},
      {x: 24.5, y: 3.5},
      {x: 3.5, y: 48.0},
      {x: 24.5, y: 48.0}
    ],
    pinout: [                   // pin positions and names
      {n: '3V3', x: 0,    y: 3.8,  s: 'left'},   // s = 'left'|'right'|'top'|'bottom'
      {n: 'GND', x: 0,    y: 6.4,  s: 'left'},
      {n: 'D23', x: 28.0, y: 3.8,  s: 'right'},
      // ...
    ]
  },
  // ...
];
```

### Categories

| Category | Icon |
|---|---|
| Microcontrollers | MCU |
| Single Board Computers | SBC |
| Sensors | SEN |
| Motors & Relays | MOT |
| Power Management | PWR |
| Wireless & RF | RF |
| Displays & Indicators | DSP |
| Integrated Circuits | IC |
| Discrete Semiconductors | SEM |
| Passives | PAS |
| Switches & Inputs | SW |
| Connectors & Hardware | CON |

### Adding Components via JSON (in-tool)

You can also use the **Community Library** button in the tool to import a JSON file of components without editing the HTML:

```json
[
  {
    "id": "my-custom-board",
    "cat": "Microcontrollers",
    "name": "My Custom Board",
    "sub": "Custom, 40×30mm",
    "w": 40, "h": 30, "pins": 20,
    "icon": "MCU", "color": "#1a3a1a",
    "holes": [{"x":3,"y":3},{"x":37,"y":3},{"x":3,"y":27},{"x":37,"y":27}],
    "pinout": [{"n":"VCC","x":0,"y":5,"s":"left"},{"n":"GND","x":0,"y":10,"s":"left"}]
  }
]
```

---

## Hosting Your Own Version

This is a single HTML file — host it anywhere static files are served:

- **GitHub Pages** (recommended): push to a public repo, enable Pages under Settings → Pages
- **Netlify Drop**: drag the HTML to [netlify.com/drop](https://app.netlify.com/drop)
- **Vercel**: `vercel --prod wire-channel-designer.html`
- **Locally**: just open the file in a browser

---

## License

MIT — do whatever you like, credit appreciated. See [LICENSE](LICENSE).

---

## Credits

- Conceived and spec'd by **Kris** / [Cerebral Meltdown Records](https://cerebralm.com)
- Component library based on community hardware specs
- Built with vanilla HTML/CSS/JS — no frameworks, no dependencies
