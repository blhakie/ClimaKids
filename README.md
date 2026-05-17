# ClimaKids
Transforming students into climate scientists through IoT sensors, gamification &amp; AI. Mobile app + bilingual game + real-time climate mapping. Measures temperature, CO₂, UV &amp; humidity. 
# ClimaKids — Unified Climate Literacy Platform 
# Live Preview https://climakids.aguiaconsultores.com/

**Empowering Mozambican youth to understand, measure, and act on climate change through real IoT sensors, gamification, and AI.**

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Android%20%7C%20iOS-green.svg)]()
[![Language](https://img.shields.io/badge/languages-PT%20%7C%20EN-orange.svg)]()

---

## Overview

ClimaKids addresses the critical gap in climate education across Mozambique — one of the world's most climate-vulnerable nations. Southern Africa is warming at approximately 1.5× the global average, yet climate literacy remains absent from school curricula.

This platform transforms students aged 10-16 into active climate data collectors and environmental agents through:

- **Real IoT sensor kits** measuring temperature, humidity, CO₂, UV index, and rainfall
- **Gamified mobile app** with missions, XP progression, and AI-powered learning
- **Collaborative climate map** visualizing community environmental data
- **Multi language educational game** with instant switching
- **Real-world impact** — student points convert to trees planted via NGO partnerships

---

## Key Features

### Mobile App (React Native)

**5 Core Screens:**
- **Home**: Personalized dashboard with weather card, XP bar, daily missions carousel, class ranking
- **Missions**: Guided IoT data collection with real-time sensor readings and step-by-step instructions
- **Climate Map**: Interactive visualization of student-collected data with urban heat island detection
- **ClimaBOT**: AI assistant providing age-appropriate climate explanations in PT/EN
- **Profile**: Progress tracking with badges, impact metrics (trees planted, data contributed), mission history

**Key Capabilities:**
- Bluetooth Low Energy integration with ESP32-based sensor kits
- Offline-first architecture with automatic sync when online
- 10-level progression system from "Explorer" to "Climate Guardian"
- Real-time class leaderboard with SVG avatar representation
- 1,000 points = 1 tree planted via New Hope Foundation partnership

### Educational Game (HTML5)

**4 Gameplay Levels:**

| Level | Name | Mechanic | Learning Objective |
|-------|------|----------|-------------------|
| 0 | **Learn** | 6-question climate quiz | Climate science fundamentals for Mozambique |
| 1 | **Build** | Green vs. polluted neighborhood simulator | Understanding urban heat islands & mitigation |
| 2 | **Crisis** | 3-phase disaster management (Cyclone) | Emergency preparedness, response & recovery |
| 3 | **Hero** | Combined challenge (unlockable) | Mastery assessment across all domains |

**Features:**
- Instant language toggle (<100ms transition)
- Lives system (3 hearts) with immediate educational feedback
- Score accumulation contributing to overall XP
- 100% offline capability with embedded fonts and inline SVG characters
- Contextual responses adapted to Inhambane and Gaza climate data

### ClimaBOT — AI Learning Assistant

Powered by **Anthropic Claude API (Haiku model)**:
- Age-appropriate language for 10-16 year olds
- Contextual responses using local weather data and student sensor readings
- 4+ quick-reply buttons for common topics (CO₂, UV Index, Heat Islands, Sensors)
- Bilingual support with seamless PT/EN switching
- Conversation logging for curriculum improvement analysis
- <4 second response time in 95% of interactions

### Collaborative Climate Map

Built with **Leaflet.js + PostGIS**:
- Real-time visualization of all student data collection points
- Color-coded pins by measurement (red = high heat, yellow = caution, green = comfortable)
- Filter by variable: temperature, air quality, rainfall, UV index
- Automatic urban heat island detection (>3°C differential between nearby zones)
- Public access mode for municipalities, researchers, and community stakeholders
- Nearest station cards showing student name, values, and time elapsed

### Teacher Portal (Laravel + React Native)

**Dashboard Features:**
- Class participation metrics: missions completed, average XP, active students
- Curriculum-aligned lesson plans linked to each mission type
- Custom mission creation with local context adaptation
- CSV bulk import for class registration (name, class, school, auto-generated PIN)
- Exportable reports in PDF and Excel formats
- Real-time climate data access for in-class analysis

**API for Research Partners:**
- REST API with anonymized aggregated data
- Municipality and university access for urban planning
- Integration-ready for INAM (National Meteorology Institute)

---

## Architecture

### System Components

```
┌─────────────────────────────────────────────────────────────┐
│                     CLIMAKIDS ECOSYSTEM                      │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────────┐      ┌──────────────┐      ┌───────────┐ │
│  │   Mobile App │◄────►│  Backend API │◄────►│ MySQL   │ │
│  │ React Native │      │   Laravel 12 │      │ + PostGIS │ │
│  └──────┬───────┘      └──────┬───────┘      └───────────┘ │
│         │                     │                              │
│         │ BLE                 │ HTTPS                        │
│         │                     │                              │
│  ┌──────▼───────┐      ┌──────▼───────┐                    │
│  │   IoT Kit    │      │  ClimaBOT AI │                    │
│  │   ESP32      │      │ Claude Haiku │                    │
│  └──────────────┘      └──────────────┘                    │
│                                                               │
│  ┌──────────────┐      ┌──────────────┐                    │
│  │ Teacher      │      │  Public Map  │                    │
│  │ Portal (SPA) │      │  (Leaflet.js)│                    │
│  └──────────────┘      └──────────────┘                    │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

### Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Mobile App** | React Native   | Cross-platform iOS/Android with OTA updates |
| **Backend** | Laravel 12 (PHP) | API, mission logic, data aggregation |
| **Database** | MySQL + PostGIS | Geospatial queries for climate mapping |
| **AI Assistant** | Anthropic Claude (Haiku) | Contextual climate education responses |
| **Climate Map** | Leaflet.js + OpenStreetMap | Interactive mapping with offline tile support |
| **Teacher Portal** | React Native | SPA integrated with Laravel backend |
| **Game Engine** | HTML5 + vanilla JS | Zero dependencies, offline-capable |
| **IoT Firmware** | Arduino Framework (C++) | ESP32 sensor communication via BLE |
| **Hosting** | VPS Ubuntu  | <200ms latency to Mozambique |
| **CI/CD** | GitHub Actions | Automated testing, building, and deployment |

---

## IoT Sensor Kit

### Hardware Specifications

| Component | Model | Measurement | 
|-----------|-------|-------------|
| Microcontroller | ESP32 DevKit V1 | WiFi + BLE + GPIO |
| Temperature & Humidity | DHT22 / SHT31 | T (°C), H (%) | 
| CO₂ Sensor | MH-Z19B (NDIR) | CO₂ (0-5000 ppm) |
| UV Sensor | GUVA-S12SD | UV Index (0-11+) |
| Rain Sensor | FC-37 / YL-83 | Presence & intensity |
| Battery | Li-Ion 3.7V 2000mAh + TP4056 | ~8h autonomy | 
| Enclosure | ABS UV-resistant (IP54) | Weather protection | 


### Firmware Features
- BLE advertising with service UUID identification
- 5-second sensor reading interval
- 90-second stability validation before allowing data submission
- OTA (Over-The-Air) firmware updates
- Low-power sleep mode when inactive
- Local data buffering for offline scenarios

---

## Original SVG Character System

All characters are **original designs** with Mozambican representation, drawn as inline SVG (no external images):

| Character | Description | Usage |
|-----------|-------------|-------|
| **Amara** | Teen girl with voluminous afro, yellow bandana, lab goggles, mint crop hoodie | Primary female avatar, ranking, map stations |
| **Tomás** | Teen boy with fade haircut zigzag line, headphones, oversized blue soccer jersey #9 | Primary male avatar, profile, "You" map pin |
| **ClimaBOT (Boto)** | Friendly robot with holographic chest panel, green LED eyes, pixelated smile | AI assistant screen avatar |
| **Sun-Dude** | Cool sun with dark sunglasses, wide smile, white rays | Weather card, UV history |
| **SensorBot** | Small IoT droid with WiFi signal arcs, green LED eyes | Mission hero, sensor history |
| **Raindrop** | Expressive water drop with white eyes, smile, dripping base | Humidity card, rain missions |
| **WindKid** | Wind spiral with central spherical face, rosy cheeks | Wind card, air quality missions |
| **Trophy** | Trophy with face, bright eyes, smile, star on cup | Mission completion reward popup |
| **MapPin** | Green map pin with white inner circle, smiley face | Field mission cards |
| **Leaf** | Green leaf with veins and face | "Eco" badge |
| **Tree** | 3-layer tree with friendly face, flying birds | "Trees Planted" impact card |
| **Flame** | Flame with golden core and face | Locked "Flame" badge |

All characters feature **age-appropriate representation**, culturally relevant styling (skin tones, hair textures, accessories), and CSS animation (floating, pulsing, bouncing).

---

## Gamification System

### XP & Points Mechanics

| Action | Reward | Details |
|--------|--------|---------|
| IoT mission completed (basic) | +30-50 XP, +10-20 pts | Depends on difficulty and sensor precision |
| Field mission (no sensor) | +20-40 XP, +8-15 pts | Visual observation, photography, questionnaire |
| Quiz question correct | +10 XP, +10 score | Per question; cumulative across 6 questions |
| Green neighborhood build | +5 XP × score | Score 0-10 multiplied by 5 |
| Crisis phase correct | +15 XP | Per phase; 3 phases = up to 45 XP |
| Badge unlocked | +25 XP (bonus) | Automatic upon meeting criteria |
| Level completed | +20 XP (bonus) | Additional completion bonus |
| 10 consecutive missions | Special badge | "10-Streak" badge + 50 XP bonus |
| 1,000 points accumulated | 1 tree planted | New Hope Foundation partnership — real physical action |

### 10 Progression Levels

1. **Explorer** (0-100 XP)
2. **Observer** (100-250 XP)
3. **Recorder** (250-500 XP)
4. **Guardian** (500-1000 XP)
5. **Analyst** (1000-2000 XP)
6. **Specialist** (2000-3500 XP)
7. **Expert** (3500-5500 XP)
8. **Champion** (5500-8000 XP)
9. **Master** (8000-12000 XP)
10. **Climate Guardian** (12000+ XP)

### Badges & Achievements

- **First Steps**: Complete first mission
- **Sensor Master**: Use 3 different sensor types
- **5-Day Streak**: Log in 5 consecutive days
- **Team Player**: Submit data to 5+ map locations
- **Quiz Champion**: Perfect score on any quiz level
- **Crisis Hero**: Complete Cyclone crisis with no lives lost
- **Eco Architect**: Build neighborhood with score ≥8
- **Climate Hero**: Unlock and complete Hero level

---

## Multi-language Toggle Architecture

The **instant language toggle** is implemented through a single JavaScript object containing all app text:

```javascript
const L = {
  pt: {
    screens: { home: "Início", missions: "Missões", ... },
    quiz: { q1: "Qual é a temperatura média anual em Maxixe?", ... },
    feedback: { correct: "Correto!", ... },
    // ... 500+ strings
  },
  // ect
};
```

**Key Features:**
- <100ms toggle transition (no page reload)
- Affects all 6 screens including active game state
- Session persistence of language choice
- Architecture ready for local languages (Changana, Macua, Sena) — just add new keys
- ClimaBOT responses automatically switch language
- Quiz, feedback, buttons, labels all update simultaneously

---

## Impact Metrics & Targets

### Pilot Phase 
- ✅ 30 students with climate literacy assessment
- ✅ 300+ missions completed (IoT + field + game)
- ✅ 90 data points on collaborative map
- ✅ 1 participating school
- ✅ 150 complete game sessions

### Year 1
- 🎯 500 active students
- 🎯 8,000 missions completed
- 🎯 500 climate data points
- 🎯 5 participating schools
- 🎯 50 trees planted via point conversion
- 🎯 1 municipality using data for public decision-making
- 🎯 5,000 game sessions

### Year 3
- 🎯 10,000 active students
- 🎯 250,000 missions completed
- 🎯 15,000 climate data points
- 🎯 100 participating schools
- 🎯 2,500 trees planted
- 🎯 10 municipalities using platform data
- 🎯 200,000 game sessions
- 🎯 12 open datasets available for research
- 🎯 5 languages available (PT + EN + 3 local)

---

## Alignment with UN SDGs

ClimaKids directly supports **4 Sustainable Development Goals**:

- **SDG 4 — Quality Education**: Active STEM learning with real data, curriculum-aligned materials
- **SDG 11 — Sustainable Cities**: Collaborative climate map generates urban heat island data for municipal planning
- **SDG 13 — Climate Action**: Climate literacy for next generation; point-to-tree conversion = direct mitigation
- **SDG 15 — Life on Land**: Community tree planting contributes to post-cyclone ecosystem recovery

**National Alignment:**
- Mozambique National Climate Change Adaptation & Mitigation Strategy (ENAMMC)
- Government 5-Year Plan 2025-2029 (STEM education & climate resilience axis)
- Green Climate Fund eligible project

---

## Roadmap

### Phase 0 — Concept  (Completed May 2026)
- [x] Concept document
- [x] Interactive HTML prototype (`climakids-app.html`)
- [x] Requirements document v2.0
- [x] Approval from partners and funders

### Phase 1 — MVP (Months 1-4)
- [ ] Android app development
- [ ] IoT Kit v1.0 (10 units)
- [ ] Backend API + database
- [ ] Basic ClimaBOT integration
- [ ] Bilingual game integration
- [ ] Pilot with 1 school (30 students)
- **Success Criteria:** ≥75% weekly retention, daily valid sensor data, teacher uses portal independently

### Phase 2 — Expansion (Months 5-9)
- [ ] Complete teacher portal
- [ ] Public climate map
- [ ] Impact system (NGO integration)
- [ ] iOS app
- [ ] 5 pilot schools
- [ ] Additional crisis scenarios in game
- **Success Criteria:** Ministry of Education approval, ≥200 weekly active users, 1 municipality using data

### Phase 3 — Scale (Months 10-18)
- [ ] Open data API
- [ ] Local languages in toggle (Changana, Macua, Sena)
- [ ] INAM (National Meteorology Institute) integration
- [ ] 50+ schools
- [ ] 500+ IoT kits
- [ ] Hero level completion
- **Success Criteria:** ≥1,000 active users, data cited by public entity, partial financial sustainability

---

## Installation & Setup

### Prerequisites
- Node.js ≥ 18.x
- PHP ≥ 8.2
- MySQL with PostGIS ≥ 3.4
- Composer
- Arduino IDE (for IoT firmware)

### Backend Setup

```bash
# Clone repository
git clone https://github.com/blhakie/climakids.git
cd climakids/backend

# Install dependencies
composer install

# Configure environment
cp .env.example .env
php artisan key:generate

# Setup database
createdb climakids
psql climakids -c "CREATE EXTENSION postgis;"

# Run migrations
php artisan migrate --seed

# Start development server
php artisan serve
```

### Mobile App Setup

```bash
cd ../mobile

# Install dependencies
npm install

# Configure environment
cp .env.example .env

# Start Expo development server
npx expo start

# Run on Android
npx expo run:android

# Run on iOS
npx expo run:ios
```

### IoT Firmware Setup

```bash
cd ../iot-firmware

# Open in Arduino IDE
arduino climakids-sensor.ino

# Configure WiFi credentials in secrets.h
# Select board: ESP32 Dev Module
# Upload to ESP32
```

### Teacher Portal Setup

```bash
cd ../teacher-portal

# Install dependencies
npm install

# Build assets
npm run build

# Portal accessible at http://localhost:8000/portal
```
 

## Contributing

We welcome contributions from developers, educators, climate scientists, and IoT enthusiasts!

### How to Contribute

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Development Guidelines

- Follow existing code style (ESLint + Prettier configured)
- Write tests for new features
- Update documentation for API changes
- Ensure offline-first compatibility
- Test on Android 8.0+ devices
- Verify bilingual content completeness (PT + EN)

### Priority Areas for Contribution

- [ ] Additional crisis scenarios (Drought, Floods, Heatwave)
- [ ] Local language translations (Changana, Macua, Sena)
- [ ] Additional quiz questions with Mozambique context
- [ ] IoT kit alternative sensor integrations
- [ ] Accessibility improvements (screen reader support)
- [ ] Climate curriculum alignment for other African nations

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

**Exception:** SVG character designs are © Águia Consultores Lda. and licensed for use within ClimaKids platform only.

---

## About Águia Consultores

**Águia Consultores Lda.** is a Mozambican consultancy specializing in climate resilience, banking agency, and software development.

- **NUIT:** 401359877
- **Webiste:** https://aguiaconsultores.com
- **Headquarters:** Maxixe / Maputo, Mozambique
- **Focus Areas:** Climate adaptation, financial inclusion, educational technology

---

## Partners & Sponsors

### Current Partners
- **New Hope Foundation** — Tree planting implementation (1,000 pts = 1 tree)
- **Ministry of Education and Culture (Mozambique)** — Curriculum alignment

### Seeking Partnerships
- **Green Climate Fund** — Climate education funding
- **INAM** (National Meteorology Institute) — Data integration
- **Municipalities** (Maputo, Maxixe, Beira) — Urban heat island data usage
- **Universities** — Research collaboration on climate data
- **Mobile Operators** — Connectivity sponsorship for schools
- **Tech Companies** — Hardware donations (tablets, sensors)

---

## Contact

**Project Inquiries:** info@aguiaconsultores.com 
**Technical Support:** info@aguiaconsultores.com    

**GitHub Issues:** For bug reports and feature requests, please use [GitHub Issues](https://github.com/blhakie/climakids/issues)

---

## Acknowledgments

- **OpenStreetMap Contributors** — Map tiles for Mozambique
- **Anthropic** — Claude API for educational AI assistance
- **Arduino Community** — ESP32 libraries and examples
- **React Native Community** — Mobile development framework
- **Laravel Community** — Backend framework and ecosystem

---

<div align="center">

**Built with ❤️ in Mozambique for a climate-resilient future**

[⭐ Star this repo](https://github.com/blhakie/climakids)

</div>
