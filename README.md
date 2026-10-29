# L7-M Compact EV — Interactive 3D CAD Engineering Viewer

A browser-based, real-time engineering visualization of an **L7-M category compact electric quadricycle**, built with Three.js (r128). The entire vehicle is procedurally modeled in code — no external models, textures, or assets.

![Category](https://img.shields.io/badge/Category-CMVR%20L7--M-4fd1ff?style=flat-square)
![Power](https://img.shields.io/badge/Peak%20Power-15%20kW%20PMSM-5ff0a8?style=flat-square)
![Range](https://img.shields.io/badge/Range-135%20km%20LFP-ffb454?style=flat-square)

---

## Live Demo

Deployed via **GitHub Pages** — open `index.html` directly or visit the published site URL.

---

## Engineering Specification

| Parameter | Value |
|---|---|
| Category | CMVR L7-M |
| Seating | 1 + 3 (dual front buckets + rear bench) |
| Footprint | 2.70 m × 1.30 m |
| Kerb Weight | 408 kg (under 450 kg L7-M limit) |
| Battery Pack Mass | 88 kg |
| Powertrain | Rear-mounted 15 kW PMSM + reduction gearbox |
| Battery | AIS-156 certified LFP, under-floor pack |
| Range | 135 km |
| Cargo | 350 L flat deck (rear bench flip-fold) |
| Top Speed | 70 km/h |

---

## 3D Model Architecture

Every sub-assembly is generated procedurally as a separate scene graph node:

- **Tubular Spaceframe Roll Cage** — welded steel tubes with radiused joints, A/B/C pillars, roof hoop, diagonal bracing, floor pan, and cross members.
- **Powertrain** — PMSM motor with stator rings and cooling fins, reduction gearbox with ribs, differential housing, half-shafts, front axle beam, independent suspension links and coil springs.
- **Wheels** — tire torus + sidewall, 5-spoke metallic rims, hub caps, vented brake discs, and orange brake calipers.
- **AIS-156 Battery Pack** — under-floor tray with 12 cell modules (48 cells total), copper bus bars, BMS module with status LED, contactors, fuse box, service disconnect, and orange high-voltage cable routing.
- **Cabin** — dual front bucket seats with bolsters, integrated headrests, stitch detailing, and seat rails; rear bench with hinge mechanism; dashboard, instrument cluster, central display, three-spoke steering wheel, pedals, and armrests.
- **Composite Shell** — matte composite body panels with clearcoat, slanted windshield, rear glass, roof solar array (30 photovoltaic cells), sliding glass doors, mirrors, fender flares, bumpers, diffuser, and charge port.

### Materials

- **Body**: `MeshPhysicalMaterial` with clearcoat, configurable roughness/metalness per paint swatch.
- **Glass**: physical glass shader — transmission `0.96`, IOR `1.52`, thickness `0.035`, clearcoat `1.0`.
- **Metals**: high-metalness steel, rim, and copper materials driven by a procedurally generated PMREM environment map.
- **Lighting**: hemisphere + directional key/fill/rim + under-glow point light, with ACES Filmic tone mapping and PCF soft shadow maps.

---

## Interaction Reference

### Panel Controls

| Control | Function |
|---|---|
| ☰ Toggle UI Panel | Slide the control sidebar in/out for a full-screen cinematic view |
| Sub-System Isolation | Isolate cage, powertrain, battery, cabin, or shell |
| Explode Sub-Systems | Smoothly lerp assemblies apart vertically |
| Slide Doors | Animate glass doors along X and Z axes |
| LED Headlights | Toggle emissive lenses + dual real spotlight beams |
| X-Ray View | Translucent body panels + wireframe chassis |
| Auto Orbit | Turntable camera rotation |
| Reset View | Return to default hero angle |
| Camera Presets | Driver POV · Top Roof View · Under-Chassis Battery View |
| Body Swatches | Slate · Blue · Crimson · Amber · White |

### Keyboard Driving

| Key | Action |
|---|---|
| `W` / `↑` | Throttle |
| `S` / `↓` | Brake / regen |
| `A` / `←` | Steer left |
| `D` / `→` | Steer right |
| Left-Click + Drag | Orbit camera |

Wheel rotation is proportional to speed; front wheels steer with Ackermann-style reduced lock at speed. Battery SOC and estimated range drain live with throttle usage and headlight draw.

---

## Telemetry HUD

- Live speedometer (km/h)
- Battery state of charge (%)
- Estimated remaining range (km)
- Drive status indicator (Standby / Driving)

---

## Technical Notes

- **Engine**: Three.js r128 (CDN)
- **Controls**: OrbitControls with damping
- **Renderer**: antialias, ACESFilmicToneMapping, PCFSoftShadowMap
- **Performance**: `requestAnimationFrame` loop with clamped delta-time; no FPS counter in the HUD
- **Responsive**: adapts sidebar and HUD to viewport width

---

## Local Development

No build step required. Open `index.html` in a modern browser, or serve locally:

```bash
python -m http.server 8080
```

Then visit `http://localhost:8080`.

---

## License

Released for demonstration and portfolio purposes.
