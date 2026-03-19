# 🎨 Portfolio — Salwa Zaaraoui · Business Data Analyst

> **Live :** [slw-z.github.io](https://slw-z.github.io)

![Status](https://img.shields.io/badge/Status-Live-brightgreen)
![HTML](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![PowerBI](https://img.shields.io/badge/Power_BI-F2C811?logo=powerbi&logoColor=black)
![SQLServer](https://img.shields.io/badge/SQL_Server-CC2927?logo=microsoftsqlserver&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-EA4B71?logo=n8n&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?logo=amazonaws&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?logo=microsoftazure&logoColor=white)
![Figma](https://img.shields.io/badge/Figma-F24E1E?logo=figma&logoColor=white)
![Framer](https://img.shields.io/badge/Framer-0055FF?logo=framer&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white)
![VSCode](https://img.shields.io/badge/VS_Code-007ACC?logo=visualstudiocode&logoColor=white)
![Qdrant](https://img.shields.io/badge/Qdrant-DC244C?logoColor=white)
![Prophet](https://img.shields.io/badge/Prophet_ML-0866FF?logo=meta&logoColor=white)

---

## 📌 Présentation

Portfolio personnel **100% standalone** — un seul fichier HTML auto-suffisant, sans framework, sans dépendance externe, sans build step.

Conçu pour refléter une double expertise **Data Engineering & Business Intelligence**, avec une identité visuelle premium inspirée des studios de design haut de gamme (Flightpath, Zenith, Logitech).

---

## 🎨 Design System

### Palette — Bronze Eclipse

| Token | Valeur | Usage |
|---|---|---|
| `--b-dark` | `#3C2A21` | Backgrounds, gradients sombres |
| `--b-mid` | `#6B4D38` | Accents secondaires |
| `--b-light` | `#8E735B` | Bordures, séparateurs |
| `--b-bright` | `#b08d6a` | Highlights, labels actifs |
| `--bg` | `#060403` | Background global |
| `--white` | `#f5f0ea` | Texte principal |

### Typographie

| Famille | Usage |
|---|---|
| **Bebas Neue** | Titres hero, sections, stats |
| **Syne** | Corps de texte, navbar, boutons |
| **DM Mono** | Labels, tags, code, navigation |

---

## 🏗️ Architecture technique

### Structure des sections

```
index.html
│
├── 🔝 Navbar full-width
│   ├── Logo carré bronze + "Portfolio / DATA ANALYST"
│   ├── Liens de navigation centrés avec soulignement animé
│   └── Bouton CV (base64 embarqué) — téléchargement direct
│
├── 🖼️ Hero — Bronze Eclipse
│   ├── Gradient #3C2A21 → #8E735B
│   ├── Titre "BUSINESS DATA ANALYST" — effet shimmer animé
│   └── Sous-ligne : Automatisation n8n & BI · Optimisation 70% · Pipelines à impact
│
├── 📡 Marquee — 20 logos défilants
│   ├── Ligne unique centrée, animation CSS infinie
│   ├── Fondu natif dans le background (#060403)
│   └── Logos SVG inline couleurs officielles
│
├── 👤 Mon Profil
│   ├── Card identité (citation + localisation)
│   ├── Bio 3 paragraphes
│   └── Cards Formation + Expérience (animated + light burst + glow hover)
│
├── 🎬 Animation interactive — Logo Jump Dashboard
│   ├── Canvas 2D — personnages cartoon avec bras, jambes, yeux qui clignent
│   ├── 5 personnages : CSV · DAX · Python · HTML · VSCode
│   ├── Séquence : attente → course → saut → atterrissage → dashboard
│   └── Dashboard Power BI live : KPIs · Bar chart · Donut · Sparkline rouge
│
├── 💼 Projets Technique
│   └── 2 cards égales — Quantum Brussels · Monitoring STIB
│
├── 📩 Contact
│   └── CTA + badge disponibilité + bouton Outlook
│
└── 🔗 Footer
    └── 3 boutons : GitHub · LinkedIn · Outlook
```

---

## ⚙️ Fonctionnalités techniques

### Curseur personnalisé
```css
#cursor { position: fixed; width: 10px; background: #fff; border-radius: 50%; }
#cursor-ring { border: 2px solid rgba(255,255,255,0.8); border-radius: 50%; }
```
Suivi en `requestAnimationFrame` avec lag élastique sur le ring (`lerp 0.1`).

### Effet Shimmer (titre hero + titre dashboard)
```css
.shimmer-title {
  background: linear-gradient(90deg, #b08d6a 0%, #ffffff 48%, #b08d6a 100%);
  background-size: 300% 100%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: shimmer 4s linear infinite;
}
```

### Glow hover — toutes les cards
```css
.acard:hover {
  border-color: rgba(176,141,106,0.5);
  box-shadow: 0 0 30px rgba(176,141,106,0.18),
              0 0 60px rgba(176,141,106,0.08),
              inset 0 0 30px rgba(176,141,106,0.04);
}
```

### Ligne lumineuse top — cards & dashboard
```css
.acard::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(to right, var(--b-dark), var(--b-bright));
  transform: scaleX(0); transform-origin: left;
  transition: transform .4s cubic-bezier(0.05, 0.61, 0.41, 0.95);
}
.acard:hover::before { transform: scaleX(1); }
```
Même effet sur le dashboard BI — la ligne se déploie dès que `.active`.

### Animation Logo Jump — Canvas 2D
```javascript
const STATE = { WAITING:0, RUNNING:1, JUMPING:2, LANDING:3, FINISHED:4 };

// Physique relative à la taille de l'écran
const runSpeed     = W * 0.006;
const gravity      = H * 0.0008;
const jumpVelocity = H * -0.025;

// Squash & stretch au saut
const stretch = 1 + Math.abs(this.vy) * 0.002;
this.scaleX = 1 / stretch;
this.scaleY = stretch;
```
Chaque personnage démarre après que le précédent soit en course — séquence un par un, boucle automatique avec pause de 2.8s.

### Dashboard Power BI live
- **KPI cards** : Data Sources · Records · Accuracy avec barres de progression animées
- **Bar chart** : une barre par personnage atterri, transition CSS `cubic-bezier`
- **Donut SVG** : segments `stroke-dasharray` animés par `transform:rotate`
- **Sparkline** : path SVG recalculé toutes les 3 frames, dégradé rouge temps réel
- **Badge LIVE** : pulse CSS rouge · **Bordure** : ligne bronze `scaleX` au `.active`

### Marquee infini
```css
.mtrack-r { animation: mr 35s linear infinite; }
@keyframes mr { from { transform: translateX(0); } to { transform: translateX(-50%); } }
/* Contenu dupliqué · fondu natif #060403 · padding 48px vertical */
```

### Musique — YouTube IFrame API
```javascript
function onYouTubeIframeAPIReady() {
  ytPlayer = new YT.Player('yt-player', {
    videoId: 'w44dlsnJ1no',
    playerVars: { loop: 1, playlist: 'w44dlsnJ1no' }
  });
}
```
> ⚠️ Requiert un contexte HTTPS — ne fonctionne pas en `file://` local.

### CV embarqué (base64)
Le fichier `.docx` est encodé en base64 et injecté dans l'attribut `href` — **zéro serveur requis**, téléchargement natif du navigateur.

### Reveal on scroll
```javascript
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.classList.remove('hidden');
  });
}, { threshold: 0.05 });
```

### Light Burst au clic
```javascript
card.style.setProperty('--cx', x + '%');
card.style.setProperty('--cy', y + '%');
// radial-gradient positionné dynamiquement via CSS custom properties
```

---

## 🛠️ Stack

| Technologie | Usage |
|---|---|
| HTML5 | Structure sémantique — fichier unique auto-suffisant |
| CSS3 | Animations, Flexbox, `has()`, `conic-gradient`, `@property` |
| JavaScript ES6+ | Curseur, Canvas 2D, physique, YouTube API, reveal |
| Canvas 2D API | Animation personnages + dashboard Power BI |
| Google Fonts CDN | Bebas Neue, Syne, DM Mono |
| YouTube IFrame API | Lecteur audio ambiance |

**Aucun framework. Aucun bundler. Aucune dépendance npm.**

---

## 📁 Déploiement

Hébergé sur **GitHub Pages** — déploiement automatique depuis la branche `main`.

```
Repository : slw-z/slw-z.github.io
Branch     : main
File       : index.html
URL        : https://slw-z.github.io
```

---

## 📬 Contact

**Salwa Zaaraoui** · Business Data Analyst · Bruxelles, Belgique

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://linkedin.com/in/salwa-zaaraoui)
[![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white)](https://github.com/slw-z)
[![Email](https://img.shields.io/badge/Outlook-0078D4?logo=microsoft-outlook&logoColor=white)](mailto:zaaraoui.salwa@live.fr)
