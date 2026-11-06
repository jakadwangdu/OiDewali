# 🪔 Diwali Gali v3 – Open-World 3D Multiplayer Browser Game

An open-world, browser-based 3D multiplayer game where real friends celebrate Diwali together across a glowing traditional Indian neighbourhood.

> **Zero AI bots policy:** Every character in a celebration room is a real human player connected via the authoritative real-time WebSocket state server and WebRTC proximity voice mesh.

---

## 🚀 Quick Start

### 1. Install & Start Server
```bash
npm install
npm start
```

### 2. Play in Browser
Open your browser to:
```
http://localhost:3000
```

To invite friends into the same celebration room, click **🔗 Copy Invite Link** or share the URL with your room code:
```
http://localhost:3000/#room=DWL-4821
```

### 3. Run Automated Integration Test Suite
```bash
node test_multiplayer.js
```

---

## 🌟 Key Architecture & Features

### 1. Authoritative Realtime Multiplayer (`server/server.js`)
- **15 Hz Tick Rate Synchronization:** Authoritative server broadcast loop (66ms) synchronizing player positions, orientations, velocities, health, active emotes, and microphone speaking states.
- **Client-Side Interpolation:** Remote players render smoothly with linear and rotational interpolation, eliminating jitter.
- **Deterministic Cracker Replication:** Ballistic arcs and fuse timers replicate across all clients upon throw.
- **Authoritative Blast Damage & Knockback Physics:**
  $$\text{Damage} = \max\left(1, \left\lfloor D_{\max} \cdot \left(1 - \frac{d}{R}\right)^{1.3} \right\rfloor\right)$$
  Computes radial knockback impulse away from the blast epicenter, triggering screen vignettes, camera shake, and telemetry toasts.
- **Target Dummy Range:** Non-AI wooden target effigy in the Mithai Bazaar surrounded by `3m`, `6m`, and `10m` ground rings for testing cracker blast radius and damage falloff.
- **Profanity-Filtered Text & Quick-Chat:** Festive quick phrases (`🪔 Shubh Deepavali!`, `🧨 Watch out!`, `🙏 Namaste`, `💃 Dance`).

### 2. WebRTC 3D Proximity Voice Chat Mesh (`public/js/network.js`, `public/js/audio.js`)
- Peer-to-peer WebRTC mesh signaling routed through the WebSocket server connection.
- 3D distance volume roll-off using Web Audio API spatial nodes.
- Real-time microphone analyzer with animated green/gold speaking aura rings above players' heads.
- Live microphone level meter in Settings.

### 3. Expanded 4-District Open World (`public/js/world.js`)
- **District 1 — Shahi Haveli Street:** Multi-story sandstone and pastel havelis with *jharokha* balconies, rooftop *chhatris*, glowing lattice windows, steps lined with flickering diyas, and overhead fairy-light canopies with animated twinkling bulbs.
- **District 2 — Shri Lakshmi Mandir Chowk:** Elevated marble temple, carved white pillars, golden *Shikhara* spire, glowing *Kalash*, intricate 5-ring Rangoli, and a 5-tier *Deepstambh* (tower of diyas).
- **District 3 — Mithai & Pataka Bazaar:** Festive market stalls (*Kaju Katli Bhandar*, *Royal Pataka Stall*, *Chai & Jalebi Corner*, *Kandil Shop*, *Lakshmi Sweets*) + the non-AI wooden target effigy.
- **District 4 — Kamal Sarovar Ghat:** Stepped stone ghat, dark-indigo reflective water pool, 24 animated floating diyas, and rising sky lanterns (*Akash Kandil*).
- **Distant Skyline & Sky:** 1600 twinkling stars, glowing full moon, and silhouettes of the glowing city skyline.

### 4. 8 Modular 3D Avatar Species (`public/js/character.js`)
1. **🧒 Chibi Kid:** Festive kurta/sherwani with golden border.
2. **🐱 Cat:** Pointed ears, cute tail, whiskers.
3. **🐼 Giant Panda:** Dual-tone black & white ears and eye rings.
4. **🐰 Bunny:** Long ears with pink inner layer and cute blush.
5. **🦊 Kitsune Fox:** Amber fur and pointed ears.
6. **🦉 Night Owl:** Luminous eyes and golden beak.
7. **🪔 Diya-Spirit:** Glowing diya body with a flickering golden flame.
8. **🕴 Neon Stickman:** Minimalist glowing silhouette.

- **7 Festive Outfit Palettes:** Gulabi Pink, Haldi Yellow, Panna Green, Aakash Blue, Baingani Purple, Bhagwa Orange, Chandni Cream.
- **3 Accessories:** Pagdi / Festive Cap, Kala Chashma (Sunglasses), and Marigold Mala (Garland).

### 5. 9 Oversized 3D Firecrackers (`public/js/crackers.js`)
Modeled at $2.2\times$ scale with distinct 3D geometry held in hand and thrown in a physics arc:
1. 🥔 **Aalu Bomb:** Twine-wrapped sphere (55 HP max, 11m blast radius, heavy ground shockwave ring, blinding flash, chest-thumping sub-bass, heavy knockback).
2. 🚀 **SkyShot:** Mortar rocket (15 HP at pad, 4m radius) that whistles into the sky and bursts into multi-ring chrysanthemum sparks.
3. 🌀 **Giant Chakri:** Flat coiled spinner (26 HP max, 6.5m radius) that spins rapidly on the ground, throwing a 360° vortex of pink and gold sparks.
4. 🌶️ **Mirchi Cluster Bomb:** Red-and-green bundle (34 HP max, 7.5m radius) that hops and detonates into 10 rapid-fire explosions.
5. ⛲ **Royal Anar:** Conical flowerpot (18 HP max, 5m radius) erupting into a towering 7m cascade of golden stars.
6. 💥 **Lakshmi Triple Bomb:** Green-and-gold foiled cylinder (75 HP max, 14m radius) that detonates in three escalating shockwaves.
7. 🧨 **1000-Wala Ladi:** Long braided garland of crackers (42 HP max, 9.5m radius) unrolling into a 28-shot chain reaction.
8. 🪁 **Patang Swirl Rocket:** Lime-green spiral rocket (16 HP max, 4.5m radius) corkscrewing upward before bursting into aerial sub-clusters.
9. ✨ **Phuljhadi:** Safe handheld golden sparkler (0 HP damage) for drawing light trails while dancing with friends.

### 6. Controls & Ergonomics (`public/js/game.js`)
- **Desktop:**
  - Movement: `W`, `A`, `S`, `D` / Arrow Keys (Hold `Shift` to sprint)
  - Camera: Mouse Look (Pointer Lock)
  - Throw Cracker: Left Mouse Click, `E`, or `F`
  - Jump: `Spacebar`
  - Select Cracker: `1` to `9` keys or Mouse Scroll Wheel
  - Toggle Camera (1st / 3rd Person): `V` key
  - Eat Kaju Katli Sweet (+35 HP): `H` key
  - Chat: `Enter` key
  - Pause: `Escape` / `P`
- **Smartphone Dual-Touch:**
  - Left virtual joystick for movement.
  - Right-half touch drag for 360° camera look.
  - Dedicated tactile action buttons: **🧨 Throw**, **🦘 Jump**, **🎥 Camera**, **🍬 Heal**.

---

## 📁 File Structure

```
DiwaliGame/
├── package.json                   # Dependencies (express, ws) and scripts
├── test_multiplayer.js            # Automated end-to-end multiplayer integration test
├── server/
│   └── server.js                  # Authoritative room state, sync, damage, chat & signaling
└── public/
    ├── index.html                 # Main single-page HTML with glassmorphism UI
    ├── css/
    │   └── style.css              # Glassmorphic styles, Baloo 2 font, responsive HUD
    └── js/
        ├── audio.js               # Procedural Web Audio synthesizer & 3D spatial panner
        ├── crackers.js            # 9 oversized 3D crackers, particle systems & shockwaves
        ├── character.js           # 8 modular avatar species & remote player visualizer
        ├── world.js               # 4-district open world, procedural textures & lighting
        ├── network.js             # WebSocket gateway & WebRTC proximity voice mesh
        └── game.js                # Core game controller, physics, minimap & UI bindings
```
"# OiDewali" 
