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
├── 🖼️ Hero — Bronze Eclipse 16:9
│   ├── Gradient #3C2A21 → #8E735B
│   ├── Titre "BUSINESS DATA ANALYST" — effet shimmer animé
│   └── Sous-ligne de stats centrée
│
├── 📡 Marquee — 20 logos défilants
│   ├── Ligne unique, animation CSS infinie
│   └── Logos SVG inline couleurs officielles
│
├── 👤 Mon Profil
│   ├── Card identité (citation + localisation)
│   ├── Bio 3 paragraphes
│   └── Cards Formation + Expérience (animated + light burst)
│
├── 💼 Projets Technique
│   └── 2 cards égales — Quantum + STIB
│
├── ⚡ Services — Expanding Flex Cards
│   ├── 4 cards CSS flex expansibles au hover
│   ├── Gradient border animé (conic-gradient rotation)
│   ├── Glow bar 85% width au hover
│   └── Images en fond overlay
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

### Effet Shimmer (titre hero)
```css
.shimmer-title {
  background: linear-gradient(90deg, #b08d6a 0%, #ffffff 48%, #b08d6a 100%);
  background-size: 300% 100%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: shimmer 4s linear infinite;
}
```

### Expanding Services Cards
```css
.options-container:has(.option:hover) .option { flex: 0.4; }
.options-container:has(.option:hover) .option:hover { flex: 3; }
/* transition: .5s cubic-bezier(0.05, 0.61, 0.41, 0.95) */
```
Utilise `:has()` CSS natif — aucun JavaScript requis.

### Light Burst au clic (cards)
```javascript
card.style.setProperty('--cx', x + '%');
card.style.setProperty('--cy', y + '%');
// radial-gradient positionné dynamiquement via CSS variables
```

### Marquee infini
```css
.mtrack-r { animation: mr 35s linear infinite; }
@keyframes mr { from { transform: translateX(0); } to { transform: translateX(-50%); } }
/* Contenu dupliqué pour boucle seamless */
```

### Musique — YouTube IFrame API
```javascript
function onYouTubeIframeAPIReady() {
  ytPlayer = new YT.Player('yt-player', {
    videoId: 'Q3ZmmKUV14o',
    playerVars: { loop: 1, playlist: 'Q3ZmmKUV14o' }
  });
}
```
> ⚠️ Requiert un contexte HTTPS — ne fonctionne pas en `file://` local.

### CV embarqué (base64)
Le fichier `.docx` est encodé en base64 et injecté directement dans l'attribut `href` du bouton — **zéro serveur requis**, téléchargement natif du navigateur.

### Reveal on scroll
```javascript
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.classList.remove('hidden');
  });
}, { threshold: 0.05 });
```

---

## 🛠️ Stack

| Technologie | Version | Usage |
|---|---|---|
| HTML5 | — | Structure sémantique |
| CSS3 | — | Animations, Grid, Flexbox, `has()`, `conic-gradient` |
| JavaScript ES6+ | — | Curseur, parallax, reveal, musique |
| Google Fonts | CDN | Bebas Neue, Syne, DM Mono |
| YouTube IFrame API | CDN | Lecteur audio de fond |

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
