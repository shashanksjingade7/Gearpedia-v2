# GearPedia

**GearPedia** is a complete gear design and validation platform — a single-file Progressive Web App (PWA) covering 21 gear types, deployed on Firebase Hosting with automatic CI/CD via GitHub Actions.

---

## What It Is

GearPedia is not a toy calculator. It is a full engineering reference and validation tool built for mechanical engineers, students, and gear designers. It implements ISO 6336 / IS 9001 / AGMA methodology with validated formulas across 21 gear families — all running offline-capable in the browser with no backend or database required.

---

## Live Site

Deployed on Firebase Hosting (Spark free plan):

- `https://gearpedia-v2.web.app`
- `https://gearpedia-v2.firebaseapp.com`

---

## Features

### Calculator Suite
A full gear design calculator accessible from the nav bar. Every calculator displays its formula alongside the result, with symbol definitions and ISO/AGMA standard references so you calculate and understand simultaneously.

### Full Gear Geometry
Computes every geometric parameter — module, pitch diameter, addendum, dedendum, centre distance, contact ratio — for all 21 supported gear types.

### Stress Analysis
Lewis bending stress and Hertz contact stress calculations with full IS / ISO 6336 compliance.

### Physical Validation
Enter measured or hand-calculated values and get an instant side-by-side comparison with GearPedia's computed results. Deviation is shown explicitly.

### Root-Cause Diagnosis
Automatically detects the most likely sources of error — wrong formula applied, unit mismatch (mm vs inch), incorrect gear ratio direction, or measurement error.

### Visual SVG Diagrams
Every gear type renders a clean, annotated SVG diagram showing tooth profile, pitch circles, and centre distance markers for visual geometry verification.

### Formula Reference Cards
Each gear type includes a complete formula reference card with IS / AGMA / DIN standard cross-references.

### Worm Gear Efficiency Calculator
Dedicated section for worm gear analysis — power loss, back-drivability, and thermal load in one place. Includes a visual gauge for efficiency output.

### Design Checklist
An interactive checklist to track gear design steps. State is persisted locally in the browser.

### Gear Comparison Tool
Side-by-side comparison of gear parameters across different configurations.

### Multi-language Support
Built-in language switcher with search, powered by Google Translate integration.

### Light / Dark Theme
Full theme system with light and dark modes, persisted across sessions.

### SI / Imperial Unit Toggle
Switch between SI and Imperial unit systems globally, with all calculations updating accordingly.

### PWA / Offline Ready
Installable as a Progressive Web App with a service worker for offline use.

---

## Supported Gear Types (21 Total)

Spur Gear, Helical Gear, Herringbone, Internal Gear, Planetary Gear, Straight Bevel, Spiral Bevel, Zerol Bevel, Miter Gear, Worm Gear, Hypoid Gear, Face Gear, Crossed Helical, Screw Gear, Spiroid Gear, Rack & Pinion, Cycloidal, Harmonic Drive, Non-Circular, Geneva Mechanism, Ratchet & Pawl.

---

## Tech Stack

| Layer | Technology |
|---|---|
| App | Vanilla HTML / CSS / JavaScript (single file) |
| Fonts | Google Fonts — Cascadia Code, Special Elite, Orbitron, Share Tech Mono |
| Animations | Canvas-based particle background |
| Diagrams | Inline SVG (dynamically generated) |
| Persistence | `localStorage` (theme, checklist, feedback) |
| Hosting | Firebase Hosting (Spark plan) |
| CI/CD | GitHub Actions |
| PWA | Web App Manifest + Service Worker |

No frameworks. No build step. No npm install. The entire app ships as one `index.html`.

---

## Repository Structure

```
Gearpedia/
├── public/
│   └── index.html          ← The entire GearPedia application
├── firebase.json           ← Firebase Hosting config (serves public/)
├── .firebaserc             ← Firebase project alias
├── .gitignore
├── .github/
│   └── workflows/
│       └── firebase-deploy.yml   ← Auto-deploy on push to main
└── README.md
```

---

## How Deployment Works

Every push to the `main` branch triggers the GitHub Actions workflow:

1. Checks out the repository
2. Installs Firebase CLI
3. Deploys the `public/` folder to Firebase Hosting

The live site updates automatically within about 60 seconds of a push.

### Firebase Hosting Config

```json
{
  "hosting": {
    "public": "public",
    "rewrites": [
      { "source": "**", "destination": "/index.html" }
    ]
  }
}
```

The `**` rewrite means all routes resolve to `index.html` — the app handles its own internal navigation via JavaScript (`showView()`).

---

## GitHub Actions — Required Secret

| Secret Name | Description |
|---|---|
| `FIREBASE_TOKEN` | Firebase CI token used to authenticate deployments |

To generate the token, run `firebase login:ci` locally and copy the output into the GitHub repository secret.

---

## Free Plan Limits (Firebase Spark)

| Resource | Free Limit |
|---|---|
| Hosting Storage | 10 GB |
| Data Transfer / month | ~10 GB (360 MB/day) |
| Custom Domain | Supported |
| SSL Certificate | Free & automatic |

The app (`index.html`) is approximately 1.2 MB. Around 8,000 page loads per day would be needed to approach the transfer limit — well within the free tier for typical usage.

---

## Local Development

No build tools needed. Just open `public/index.html` directly in a browser.

To test the Firebase deployment locally:

```bash
npm install -g firebase-tools
firebase login
firebase serve
```

To deploy manually without GitHub Actions:

```bash
firebase deploy --only hosting
```

---

## Pages / Views

The app uses a single-page view system (`showView()` in JavaScript). The main views are:

- **Home** — landing page with gear type browser, features, formulas, worm calculator, checklist, and comparison sections
- **Calculator Suite** — full multi-gear calculator with formula references
- **Feedback** — user feedback submission form
- **Dashboard** — admin view for reviewing submitted feedback and subscribers

Navigation is handled entirely client-side. All data (feedback, checklist state, theme) is stored in `localStorage`.

---

## Roadmap / Planned Development

Features under consideration for future development (to be discussed and prioritised):

- [ ] Backend integration for persistent feedback and subscriber storage
- [ ] User authentication and saved calculation history
- [ ] PDF export of calculation results and formula reference cards
- [ ] 3D gear visualisation
- [ ] Additional gear standards (DIN, JIS)
- [ ] Gear train / multi-stage system calculator
- [ ] API for programmatic gear calculations

---

## Contributing

This project is currently in active development. If you have suggestions, use the Feedback form on the live site, or open an issue on the repository.

---

## License

All rights reserved. GearPedia is a proprietary application. Unauthorised copying, distribution, or modification is not permitted without explicit written consent from the author.
