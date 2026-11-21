# 💧 Flowstate — A Navier–Stokes Fluid Sandbox

A single-file HTML5 fluid dynamics sandbox that solves **real incompressible
Navier–Stokes** on the GPU. Pour coloured fluid into an open space, watch it
curl and collide with itself, and **draw your own walls** — the fluid has to
flow around whatever you draw, or stay trapped inside it.

## 🧮 The actual physics

Every frame runs a full GPU solver — this is not a particle fake:

- **Semi-Lagrangian advection** of velocity and dye
- **Jacobi viscosity diffusion** (the slider changes how many passes run)
- **Vorticity confinement** — the swirl term that makes it roll up
- **Divergence** computation
- **Pressure solve** — 20 iterations of Jacobi
- **Pressure gradient subtraction** — projects the field to be divergence-free
- **Solid-aware backtrace** — the advection walk stops at the first solid cell,
  so fluid physically cannot jump over a drawn wall

## 🎮 How to Play

1. Click **START**
2. **Drag** anywhere to pour fluid — the faster you drag, the more momentum
   it carries
3. Hold **SPACE** for a **pressure jet** — 5× the fluid, blasted outward
4. Click the **✏ pencil** next to FLOWSTATE, then drag to **draw a shape**
   — it becomes a solid wall the fluid flows around
5. The **eraser** and the **5 thickness** buttons let you carve out gaps
6. Fiddle with **VISCOSITY** (thin wispy ↔ thick creamy), **TIMESTEP**
   (dreamy slow-mo ↔ streaked fast) and **GRAVITY** (down / off / up)
7. Press **V** to see the live velocity field

## 🎨 Fluids

Pick a colour with `1`–`6`, or the **ALL** swatch which pours every colour in
the palette at once — cyan, magenta, amber, lime and blood red, and any colour
added later.

## 🌐 Play Online

👉 **[https://nimblecozmo.github.io/flowstate/](https://nimblecozmo.github.io/flowstate/)**

## 📁 Local Play

No build step, no dependencies — it is one HTML file:

```bash
# just open it
xdg-open index.html

# or serve it
python3 -m http.server 8000
# then visit http://localhost:8000
```

> Needs **WebGL2** with floating-point textures (`EXT_color_buffer_float`).
> Chrome, Brave, Firefox and Safari 15+ all support it.

## 🛠️ Built With

Plain HTML, CSS and JavaScript in a single `index.html`. WebGL2 fragment
shaders for the whole solver, Canvas 2D overlay for the drawing and UI,
procedurally generated sound (no audio files), no external assets.
