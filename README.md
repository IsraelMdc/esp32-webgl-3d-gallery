# 🏛️ Interactive 3D Virtual Gallery & Embedded IoT Web Server

[![WebGL](https://img.shields.io/badge/WebGL-Three.js_r160-black?logo=three.js)](https://threejs.org/)
[![ESP32](https://img.shields.io/badge/Hardware-ESP32_DevKit_v1-red?logo=espressif)](https://www.espressif.com/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PlatformIO](https://img.shields.io/badge/PlatformIO-Build_Passing-orange?logo=platformio)](https://platformio.org/)

> An ultra-optimized, real-time 3D Neoclassical Virtual Gallery built with **Three.js (WebGL)** and engineered to be hosted either on modern static CDNs or served directly from the SPI Flash memory of a low-cost **ESP32 microcontroller** (4MB Flash / 320KB RAM).

---

## 🚀 Live Demo & Showcase

- 🌐 **Interactive Web Demo:** [https://israelmdc.github.io/esp32-webgl-3d-gallery/](https://israelmdc.github.io/esp32-webgl-3d-gallery/)
- 📱 **Mobile & Desktop Ready:** 60 FPS guaranteed on modern smartphones and browsers.

---

## 🌟 Key Engineering Highlights

### 1. 3D Computer Graphics (WebGL / Three.js)
- **Monumental 360° Rotunda Architecture:** Procedural 7.5m radius circular gallery with Carrara marble tiling, velvet runners, and an open celestial oculus.
- **PBR Shaders & Realistic Materials:** Physically Based Rendering with calibrated *roughness*, *metalness*, and environment reflections.
- **Botanical 3D Models (GLTF / GLB):** Seamless integration of high-fidelity botanical models (roses, lilies, gerberas) loaded asynchronously with smooth bounding-box normalizations.
- **Instanced Geometry (`InstancedMesh`):** Particle systems and 380+ organic grass tufts grouped into single draw calls, minimizing GPU driver overhead.
- **Lighting & Atmosphere:** Mixed lighting setup featuring point lights with exponential decay for candles, ambient fill, and a central rotating golden mandala with ascending uplight under the floating centerpiece.
- **Mathematical Collision System:** First-person character controller using Oriented Bounding Boxes (OBB) with sliding response physics across obstacles and furniture.

### 2. Embedded Systems & IoT Engineering (ESP32 / C++)
- **Zero External Server Dependency:** Entire WebGL runtime, GLTF models, audio synthesizer, textures, and assets are stored and delivered directly from the ESP32 SPI Flash partition.
- **Custom Flash Partitioning (LittleFS):** 2.62 MB allocated to the filesystem (`partitions.csv`), housing the compressed 3D application.
- **On-the-Fly Transparent Gzip Streaming:** Firmware streams pre-compressed `.gz` assets with automatic `Content-Encoding: gzip` injection, offloading decompression to the client's browser and conserving the ESP32's 320 KB heap.
- **Hardware-Software Bridge:** Physical GPIO 0 (BOOT button) interrupts trigger real-time particle rain in the web interface; onboard LED pulses confirm visitor interaction.

### 3. Procedural Audio Engine
- **Web Audio API Synthesizer:** Procedural music box synthesizer operating in real-time on a pentatonic scale, with no external MP3 streaming dependencies.
- **Tactile Switch Sound FX:** Dynamic mechanical audio generated using transient low-frequency impulses for the 3D wall light switch.

---

## 📁 Repository Structure

```text
├── index.html               # Main WebGL viewport and welcome glassmorphism modal
├── historia.html            # Individual station narrative viewer
├── memorias.json            # Dynamic content schema (exhibitions, titles, text)
├── css/
│   └── estilo.css           # Responsive mobile-first stylesheet & HUD overlays
├── js/
│   ├── app.js               # Application bootstrap, resize listeners & render loop
│   ├── galeria.js           # Neoclassical 3D scene builder & procedural textures
│   ├── controles.js         # Hybrid FPS controls (Pointer Lock + Touch Joystick)
│   ├── interacao.js         # Raycasting engine & modal managers
│   ├── flores_realistas.js  # GLTF/GLB loader & botanical material shaders
│   ├── abertura.js          # Intro modal orchestrator & Web Audio music box
│   └── surpresa.js          # Physical GPIO event listener
├── fotos/                   # Curated high-resolution exhibition artwork
├── modelos/                 # Low-poly botanical GLB 3D assets
├── vendor/                  # Bundled Three.js (ES Module) & GLTFLoader
├── firmware_esp32/          # C++ PlatformIO firmware, LittleFS and partition table
│   ├── src/main.cpp         # Async HTTP server & hardware interrupt handlers
│   ├── platformio.ini       # Microcontroller build definitions
│   └── partitions.csv       # Custom 2.62MB SPI Flash partition table
└── docs/                    # Detailed technical documentation
    ├── 01_ARQUITETURA_3D.md # Mathematical scene specs & shader architecture
    ├── 02_MANUAL_ESP32.md   # Flashing guide, pinout and hardware wiring
    ├── 03_GUIA_HOSPEDAGEM.md# Deployment instructions (GitHub Pages / Vercel)
    └── 04_GUIA_BLENDER.md   # Blender 3D export & optimization pipeline
```

---

## 💻 Getting Started Locally

### Running the Web Client
No package manager required. Serve the root directory using any local HTTP server:

```bash
# Python:
python -m http.server 8000

# Node.js:
npx serve .
```
Navigate to `http://localhost:8000`.

---

## 🔌 Flashing the ESP32 Firmware

1. Install [PlatformIO](https://platformio.org/) (CLI or VS Code extension).
2. Connect your **ESP32 DevKit v1** via micro-USB.
3. Configure your local Wi-Fi credentials in `firmware_esp32/src/config.h`.
4. Upload firmware and filesystem:

```bash
cd firmware_esp32

# Compile and upload C++ firmware
pio run -t upload

# Flash LittleFS partition
pio run -t uploadfs
```

---

## 🛠️ Tech Stack

- **Graphics:** Three.js, WebGL, GLTF 2.0, Canvas 2D
- **Embedded:** C++, Arduino Framework, ESP32, LittleFS, PlatformIO
- **Audio:** Web Audio API (Procedural Oscillators & Gain Nodes)
- **Deployment:** GitHub Pages, Cloudflare Tunnel, Vercel

---

## 👨‍💻 Author

**Israel Magalhães**  
- GitHub: [@IsraelMdc](https://github.com/IsraelMdc)  
- LinkedIn: [linkedin.com/in/israelmdc](https://www.linkedin.com/in/israelmdc/)

Distributed under the **MIT License**.
