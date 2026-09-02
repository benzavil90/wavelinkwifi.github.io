from pathlib import Path
import zipfile, textwrap

root = Path("/mnt/data/mapozi-wifi-glitter-page")
(root / "assets").mkdir(parents=True, exist_ok=True)

index_html = r"""<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mapozi WiFi - Payment Successful</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <main class="page">
    <section class="card">
      <header class="brand">
        <div class="logo-mark">
          <div class="wifi">⌁</div>
          <div class="m-letter">M</div>
        </div>
        <div class="brand-name">MAP<span>O</span>Zi</div>
        <div class="wifi-text">WiFi</div>
      </header>

      <section class="success-panel">
        <div class="check">✓</div>
        <h1>Payment Successful!</h1>
        <p>Thank you for choosing Mapozi WiFi.</p>
        <p>Your internet access is now active.</p>

        <!-- Animated multi-colour glittering star -->
        <div class="star-stage" aria-label="Glittering Thank You star">
          <canvas id="stars"></canvas>
          <div class="thank-you">
            <div>THANK</div>
            <div>YOU!</div>
          </div>
        </div>

        <button class="continue-btn" onclick="continueToInternet()">
          <span class="globe">◎</span>
          Continue to Internet
        </button>

        <div class="help-box">
          <div class="headset">◉</div>
          <div>
            <h2>Need Help?</h2>
            <p>Contact us on WhatsApp or Call</p>
            <strong>◉ 0111 442 002</strong>
          </div>
        </div>
      </section>

      <div class="tagline">Fast • Affordable • Reliable</div>
    </section>
  </main>

  <footer>🔒 &nbsp; Secure Connection</footer>
  <script src="script.js"></script>
</body>
</html>
"""

style_css = r"""* {
  box-sizing: border-box;
}

:root {
  --blue: #075cff;
  --dark-blue: #071c45;
  --green: #12a85b;
}

html, body {
  margin: 0;
  min-height: 100%;
  font-family: Arial, Helvetica, sans-serif;
}

body {
  background:
    repeating-linear-gradient(25deg, rgba(38, 126, 226, .10) 0 2px, transparent 2px 34px),
    #dcecff;
  color: var(--dark-blue);
}

.page {
  padding: 46px 18px 20px;
}

.card {
  width: min(920px, 100%);
  margin: auto;
  padding: 38px 9% 28px;
  background: rgba(255,255,255,.97);
  border-radius: 30px;
  box-shadow: 0 12px 40px rgba(0, 49, 110, .13);
}

.brand {
  text-align: center;
  margin-bottom: 26px;
}

.logo-mark {
  width: 150px;
  height: 130px;
  margin: auto;
  position: relative;
}

.m-letter {
  position: absolute;
  left: 50%;
  top: 36px;
  transform: translateX(-50%);
  font-size: 104px;
  line-height: .8;
  font-weight: 900;
  font-style: italic;
  color: #071b45;
}

.wifi {
  position: absolute;
  z-index: 2;
  left: 50%;
  top: -5px;
  transform: translateX(-50%) rotate(-2deg);
  font-size: 88px;
  font-weight: 900;
  color: #0872f8;
  line-height: .6;
}

.brand-name {
  font-size: clamp(42px, 7vw, 70px);
  font-weight: 900;
  letter-spacing: 3px;
  color: #071b45;
}

.brand-name span {
  color: #0872f8;
}

.wifi-text {
  margin-top: -5px;
  font-size: 28px;
  letter-spacing: 7px;
  font-weight: 700;
  color: #0872f8;
}

.success-panel {
  border: 1px solid #e7eaf0;
  border-radius: 28px;
  padding: 26px 4% 24px;
  text-align: center;
  box-shadow: 0 5px 20px rgba(0,0,0,.06);
}

.check {
  width: 92px;
  height: 92px;
  margin: 0 auto 12px;
  border: 6px solid var(--green);
  border-radius: 50%;
  display: grid;
  place-items: center;
  color: var(--green);
  font-size: 62px;
  font-weight: 700;
}

h1 {
  margin: 0 0 16px;
  color: var(--green);
  font-size: clamp(34px, 5vw, 48px);
}

.success-panel > p {
  margin: 5px 0;
  font-size: clamp(18px, 2.5vw, 25px);
}

/* Star area */
.star-stage {
  position: relative;
  width: min(650px, 100%);
  height: 390px;
  margin: 22px auto 10px;
  overflow: hidden;
  border-radius: 14px;
  background: #000;
}

#stars {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

.thank-you {
  position: absolute;
  inset: 0;
  display: grid;
  place-content: center;
  gap: 4px;
  color: #ffd85a;
  text-shadow:
    0 0 6px #fff2a8,
    0 0 14px #ffbd27,
    2px 2px 0 #8d5a00;
  font-family: Georgia, "Times New Roman", serif;
  font-weight: 900;
  font-size: clamp(45px, 8vw, 76px);
  line-height: .95;
  letter-spacing: 2px;
}

.continue-btn {
  width: 100%;
  border: 0;
  border-radius: 18px;
  padding: 20px;
  background: linear-gradient(90deg, #075cff, #176efb);
  color: white;
  font-size: clamp(21px, 3vw, 30px);
  font-weight: 700;
  cursor: pointer;
  box-shadow: 0 7px 16px rgba(0, 91, 255, .2);
}

.continue-btn:hover {
  filter: brightness(1.08);
}

.globe {
  font-size: 34px;
  margin-right: 10px;
}

.help-box {
  margin-top: 18px;
  padding: 22px;
  border-radius: 18px;
  background: #eaf4ff;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 25px;
  text-align: left;
}

.headset {
  font-size: 62px;
  color: #0764e9;
}

.help-box h2 {
  margin: 0 0 10px;
  color: #0764e9;
  font-size: 28px;
}

.help-box p {
  margin: 0 0 7px;
  font-size: 20px;
}

.help-box strong {
  color: #0764e9;
  font-size: 28px;
}

.tagline {
  text-align: center;
  color: #0872d8;
  font-weight: 700;
  font-size: 23px;
  margin-top: 24px;
}

footer {
  background: #062b5d;
  color: white;
  text-align: center;
  padding: 20px;
  font-size: 18px;
}

@media (max-width: 600px) {
  .page { padding: 18px 10px; }
  .card { padding: 24px 12px; border-radius: 22px; }
  .star-stage { height: 300px; }
  .help-box { gap: 12px; }
  .headset { font-size: 45px; }
  .help-box h2 { font-size: 22px; }
  .help-box p { font-size: 16px; }
  .help-box strong { font-size: 22px; }
}
"""

script_js = r"""const canvas = document.getElementById("stars");
const ctx = canvas.getContext("2d");

let particles = [];
const colors = [
  "#ffffff", "#ffd166", "#ff9f1c", "#ff4d6d",
  "#00e5ff", "#54ff9f", "#9b7bff", "#ff72e0"
];

function resize() {
  const dpr = Math.min(window.devicePixelRatio || 1, 2);
  canvas.width = canvas.clientWidth * dpr;
  canvas.height = canvas.clientHeight * dpr;
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
  createParticles();
}

function createParticles() {
  const w = canvas.clientWidth;
  const h = canvas.clientHeight;
  particles = [];

  // Particles arranged around a large five-point star.
  const points = [];
  const cx = w / 2, cy = h / 2;
  const outer = Math.min(w, h) * .42;
  const inner = outer * .42;

  for (let i = 0; i < 10; i++) {
    const r = i % 2 === 0 ? outer : inner;
    const a = -Math.PI / 2 + i * Math.PI / 5;
    points.push({ x: cx + Math.cos(a) * r, y: cy + Math.sin(a) * r });
  }

  for (let i = 0; i < points.length; i++) {
    const a = points[i];
    const b = points[(i + 1) % points.length];
    const distance = Math.hypot(b.x - a.x, b.y - a.y);
    const count = Math.floor(distance / 4);

    for (let j = 0; j < count; j++) {
      const t = j / count;
      particles.push({
        x: a.x + (b.x - a.x) * t + (Math.random() - .5) * 5,
        y: a.y + (b.y - a.y) * t + (Math.random() - .5) * 5,
        size: 1 + Math.random() * 2.6,
        color: colors[Math.floor(Math.random() * colors.length)],
        phase: Math.random() * Math.PI * 2,
        speed: .025 + Math.random() * .08
      });
    }
  }
}

function drawSpark(x, y, size, color, alpha) {
  ctx.save();
  ctx.globalAlpha = alpha;
  ctx.strokeStyle = color;
  ctx.fillStyle = color;
  ctx.shadowColor = color;
  ctx.shadowBlur = 10 * size;

  ctx.beginPath();
  ctx.moveTo(x, y - size * 5);
  ctx.lineTo(x, y + size * 5);
  ctx.moveTo(x - size * 5, y);
  ctx.lineTo(x + size * 5, y);
  ctx.stroke();

  ctx.beginPath();
  ctx.arc(x, y, size * 1.1, 0, Math.PI * 2);
  ctx.fill();
  ctx.restore();
}

function animate(time) {
  const w = canvas.clientWidth;
  const h = canvas.clientHeight;
  ctx.clearRect(0, 0, w, h);

  for (const p of particles) {
    const twinkle = (Math.sin(time * p.speed + p.phase) + 1) / 2;
    const alpha = .35 + twinkle * .65;
    drawSpark(p.x, p.y, p.size * (.7 + twinkle), p.color, alpha);
  }

  requestAnimationFrame(animate);
}

function continueToInternet() {
  // Change this to your hotspot/login URL.
  window.location.href = "#internet";
}

window.addEventListener("resize", resize);
resize();
requestAnimationFrame(animate);
"""

readme = r"""# Mapozi WiFi Payment Success Page

A responsive HTML/CSS/JavaScript version of the supplied Mapozi WiFi confirmation design.

## Features

- Responsive mobile and desktop layout
- Mapozi WiFi branding
- Payment successful section
- No username/package/start/expiry information
- Black glittering five-point star
- Animated glitter particles in multiple colours:
  - Gold
  - White
  - Orange
  - Pink
  - Cyan
  - Green
  - Purple
- Continue to Internet button
- Help/WhatsApp section

## Run locally

Open `index.html` in a browser.

## GitHub Pages

1. Create a new GitHub repository.
2. Upload `index.html`, `style.css`, and `script.js`.
3. Go to **Settings → Pages**.
4. Select the main branch and `/root`.
5. Save and open the generated GitHub Pages URL.

## Change the Internet button

Edit `continueToInternet()` in `script.js` and replace:

```js
window.location.href = "#internet";
```

with your actual captive portal/hotspot URL.
"""

# Write files
(root / "index.html").write_text(index_html, encoding="utf-8")
(root / "style.css").write_text(style_css, encoding="utf-8")
(root / "script.js").write_text(script_js, encoding="utf-8")
(root / "README.md").write_text(readme, encoding="utf-8")

zip_path = Path("/mnt/data/mapozi-wifi-glitter-page.zip")
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for f in root.rglob("*"):
        if f.is_file():
            z.write(f, f.relative_to(root))

print(f"Created GitHub-ready project: {zip_path}")
