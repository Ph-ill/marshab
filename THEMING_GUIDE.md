# MarsHab Theming Guide (SSID, Credentials & Hardware Notes)

Since this game is meant to be a personalized gift for the 8 people on the SpaceX ACE team, the actual Pico W hardware needs slight flash-time customization.

Use this guide when configuring `boot.py` or `main.py` on the Pico W firmware for each recipient.

---

## 1. Network Personalization (Captive Portal)

Each Pico W acts as a unique WiFi hotspot. By default, it might be named `MarsHab-Demo`. Change this per-recipient so they easily spot their own habitat when plugging it in on their desk.

### Example configs

**Avery's Hab**
- **SSID:** `MarsHab-Avery` or `ACE-Hab-Avery`
- *No password recommended* so visitors (other colleagues) can connect seamlessly in the office, relying on the browser's game PIN for actual game login.

**Sam's Hab**
- **SSID:** `MarsHab-Sam`

If your backend code requires hardcoded initialization of the `habId`, use clear unique IDs: `hab_avery`, `hab_sam`, etc.

## 2. Setting up the owner PIN initially (Optional)

The UI allows for "Unclaimed Hab" setup directly in the browser. When a recipient connects for the very first time, they will see:
- "Unclaimed Hab module"
- "Claim Hab & Setup PIN"

They will customize their own base suit color, skin tone, and choose a PIN right from their phone.
*You shouldn't need to hardcode PINs on the backend* for them, provided the `MockServer` `/api/setup` endpoint behavior is faithfully replicated on your real Python backend.

## 3. In-Jokes & Catalog Customization

Right now, `index.html` has a hardcoded item `CATALOG`.
If you want to personalize items for specific people (e.g., adding an item that only makes sense to the ACE team):

Open `src/index.html` and modify the `CATALOG.items` dictionary.
```json
  "coffee_mug": { kind:'furniture', name:'Morning Fuel', price:10, footprint:[1,1], frame:'mug_sprite', color:'#d9d9d9' },
```

**Important:** Because all players expect the catalog to be identical across devices so that gifts render properly when visiting, **you must ensure every Pico W receives the exact same `index.html` catalog**. Don't create an item that only exists in Avery's catalog, otherwise it will render invisibly or fail when carried to Sam's hab.

## 4. Flash and Play

1. Flash the MicroPython runtime onto the Pico W.
2. Transfer your backend `.py` scripts (`main.py`, captive portal logic, API routes).
3. Transfer the *gzipped* front-end files to the Pico's LittleFS storage:
   - Compress `src/index.html` -> `index.html.gz`
   - Store it as `index.html.gz` but serve it with `Content-Encoding: gzip` and `Content-Type: text/html`.
4. Power cycle the Pico. Connect your phone to the new SSID and verify the portal launches.
