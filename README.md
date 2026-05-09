# Shot Viewer

A browser-based 3D camera tool for AI video production. Load a GLB model, select a shot preset, and export a 16:9 screenshot with the exact Flow/Veo conversion prompt — ready to use.

No build step. No install. One file.

---

## How it works

### The pipeline problem

AI video generators like Veo need a reference image to understand who the subject is and how to frame the shot. A flat photo works for standard angles, but for complex camera positions — bird's eye, low angle, over the shoulder — the model has no spatial information to work from. It guesses, and it guesses wrong.

Shot Viewer solves this by letting you position a 3D model of your subject at any camera angle, export a clean 16:9 screenshot, and convert it to photorealistic in Google Flow before it ever reaches Veo.

### Step by step

**1. Generate your 3D model in Meshy**
Upload a full-body photo at [meshy.ai](https://meshy.ai) → Image to 3D. Use Meshy 5 on the free plan. No export needed — the GLB download works with this tool.

**2. Load the GLB here**
Drag your `.glb` file into the viewport or click Browse. The model loads directly in the browser — nothing is uploaded anywhere.

**3. Select a shot preset**
Choose from 8 built-in presets. The camera animates to the correct position automatically:

| Shot | Camera position |
|---|---|
| Full Body Standard | Frontal, eye level |
| American Shot | Knees up, frontal |
| Close-Up | Chest up, tight |
| Three Quarters | 45° rotation, full body |
| Low Angle | Ankle height, looking up |
| Bird's Eye | Directly above, looking down |
| Over the Shoulder | Behind right, shoulder in foreground |
| Dutch Tilt | Frontal, 15° camera roll |

**4. Add custom shots**
Click **+ New shot** to define your own camera position with X·Y·Z coordinates and a custom Flow prompt. Custom shots persist for the session.

**5. Screenshot**
Click **Screenshot** in the footer. Downloads a PNG of the current 16:9 viewport at full resolution.

**6. Convert to photorealistic in Flow**
Open [Google Flow](https://flow.google.com). Upload your screenshot. Use the prompt from the right panel — it's specific to the shot you're on. Click **Copy prompt** to grab it.

**7. Generate the video in Veo**
Upload the photorealistic conversion plus your composite (subject + environment) as references. The screenshot gave Veo the camera geometry. The composite gives it the world.

---

## Built-in shots and what they're for

**Full Body Standard** — the master reference. Use this for every Veo generation unless you need a specific angle. Frontal, eye level, full body visible.

**American Shot** — dialogue scenes, walking sequences, social media vertical video. Frames from knees up.

**Close-Up** — emotional moments, face-forward content, music videos. Frames from chest up.

**Three Quarters** — more cinematic than frontal. Adds depth and dimension to any static or walking shot.

**Low Angle** — power, scale, drama. Camera at ankle height looking up. Buildings, night sky, and subject looming large.

**Bird's Eye** — overhead walking sequences, atmospheric establishing shots. Camera directly above looking straight down.

**Over the Shoulder** — conversation scenes, POV shots, narrative sequences. Subject's shoulder in foreground, scene ahead.

**Dutch Tilt** — tension, disorientation, psychological unease. Standard frontal framing with 15° camera roll.

---

## Custom shot coordinates

When adding a custom shot, the coordinate system is:

- **Y** = height. `0` is ground level. A standing person's head is around `1.7–1.8`.
- **Z** = distance from subject. Positive = in front. Negative = behind.
- **X** = left/right offset. `0` is centered.

Example — extreme close-up on face:
```
Position:  x=0  y=1.75  z=0.6
Target:    x=0  y=1.75  z=0
```

Example — worm's eye (looking straight up from ground):
```
Position:  x=0  y=0.02  z=0.01
Target:    x=0  y=2.0   z=0
```

---

## Deploy to GitHub Pages

1. Fork or create a new repo
2. Add `index.html` to the root
3. Go to **Settings → Pages → Branch: main → Save**
4. Your tool is live at [`https://yourusername.github.io/your-repo`](https://github.com/miguelcastroe/shotmaker)

No configuration needed. The CDN dependencies load automatically on first use.

---

## Dependencies

Loaded via CDN at runtime — no installation required.

- [Three.js r128](https://threejs.org)
- GLTFLoader r128
- OrbitControls r128

---

## Part of a larger pipeline

Shot Viewer is one step in a full AI video production workflow:

```
Gemini          →  your photorealistic likeness
Meshy           →  3D body geometry for complex angles
Shot Viewer     →  camera positioning + screenshot export
Google Flow     →  photorealistic conversion of 3D screenshots
Photoshop       →  subject + environment compositing
Veo             →  final video generation
```

---

*Built for personal AI video production. One HTML file, zero dependencies, works offline after first load.*
