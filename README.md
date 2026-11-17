<p align="center">
  <img src="assets/hero_banner.png" alt="YouTube Data Video Factory" width="100%">
</p>

<h1 align="center">YouTube Data Video Factory</h1>

<p align="center">
  <b>An autonomous AI studio that finds trending topics, researches and verifies real data, renders broadcast-quality<br>
  animated videos (Shorts, long-form and 3D), designs the thumbnail, writes the SEO metadata and publishes to YouTube.</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/Rendering-Pillow%20%2B%20NumPy-8B5CF6">
  <img src="https://img.shields.io/badge/Video-FFmpeg-007808?logo=ffmpeg&logoColor=white">
  <img src="https://img.shields.io/badge/LLMs-Groq%20%7C%20Gemini-F59E0B">
  <img src="https://img.shields.io/badge/YouTube-Data%20%7C%20Analytics%20%7C%20Reporting%20API-FF0000?logo=youtube&logoColor=white">
  <img src="https://img.shields.io/badge/DB-SQLite-003B57?logo=sqlite&logoColor=white">
  <img src="https://img.shields.io/badge/CI-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white">
</p>

> **Note:** this is a showcase repository: screenshots, sample renders and architecture only.
> The source code is private; a live walkthrough is available on request.

---

## At a glance

| | |
|---|---|
| **One click → published video** | Topic discovery, research, fact-check, render, thumbnail, metadata, upload, engagement comment and series playlist, all without manual work. |
| **3 video formats** | 9:16 Shorts bar-chart races · 16:9 long-form races with story beats · 3D "pillar" comparisons with a perspective camera. |
| **Real data, not invented data** | Official sources first (SEC EDGAR, FAOSTAT, OWID / World Bank, Wikipedia tables), then a multi-model fact-check gate. |
| **Self-improving** | YouTube Analytics and Reporting API results feed back into topic ranking, so the system learns what this audience watches. |
| **Results** | 113+ videos rendered · **13.6K views in the last 28 days (+486%)** · 2,079 watch-minutes · 38 uploads in the period. |

---

## Sample output

### Shorts (9:16, 60 fps)

<p align="center">
  <img src="assets/gifs/short_ronaldo_vs_messi.gif" width="30%">
  <img src="assets/gifs/short_coffee_producers.gif" width="30%">
  <img src="assets/gifs/short_nfl_passing_yards.gif" width="30%">
</p>

▶️ Full-quality clips: [Ronaldo vs Messi](assets/videos/short_ronaldo_vs_messi.mp4) · [Coffee producers](assets/videos/short_coffee_producers.mp4) · [NFL passing yards](assets/videos/short_nfl_passing_yards.mp4)

<p align="center"><img src="assets/gallery_shorts.png" width="90%"></p>

### Long-form (16:9, 60 fps)

<p align="center">
  <img src="assets/gifs/long_gdp_race.gif" width="32%">
  <img src="assets/gifs/long_social_media_ad_revenue.gif" width="32%">
  <img src="assets/gifs/long_coffee_producers.gif" width="32%">
</p>

▶️ Full-quality clips: [GDP race](assets/videos/long_gdp_race.mp4) · [Social media ad revenue](assets/videos/long_social_media_ad_revenue.mp4) · [Coffee producers](assets/videos/long_coffee_producers.mp4)

Auto-designed thumbnails:

<p align="center"><img src="assets/gallery_longform.png" width="95%"></p>

### 3D comparisons (16:9, 3D camera written from scratch)

<p align="center">
  <img src="assets/gifs/3d_richest_companies.gif" width="32%">
  <img src="assets/gifs/3d_cruise_ships.gif" width="32%">
  <img src="assets/gifs/3d_billionaire_countries.gif" width="32%">
</p>

▶️ Full-quality clips: [Richest companies](assets/videos/3d_richest_companies.mp4) · [Cruise ships](assets/videos/3d_cruise_ships.mp4) · [Billionaire countries](assets/videos/3d_billionaire_countries.mp4)

<p align="center"><img src="assets/gallery_3d.png" width="95%"></p>

The 3D engine uses no Blender or Unity. It is a pinhole-camera renderer built on NumPy and Pillow: perspective-warped textures,
parallax scenery, waving flags, a drone-style intro, and a podium finale with glow, confetti and synthesized sound design.
An LLM designs each scene to match the topic (snowy mountains for ski resorts, desert for oil, city at night for money).

<p align="center">
  <img src="assets/quality/3d_ai_scene_themes.jpg" width="49%">
  <img src="assets/quality/3d_camera_frames.jpg" width="49%">
</p>

---

## Control center (dashboard)

| | |
|---|---|
| <img src="assets/dashboard/01_control_center.png"> | <img src="assets/dashboard/02_topic_categories.png"> |
| **Content intelligence engine:** one-click trend scans, best-topic research and fully autonomous pipelines. | **Categories and custom topics:** pick a niche or type any question. |
| <img src="assets/dashboard/03_preview_player.png"> | <img src="assets/dashboard/04_metadata_bundle.png"> |
| **Preview and publish:** review the render and the AI thumbnail, then publish in one click. | **AI metadata bundle:** title, description, tags, sources and the engagement comment. |
| <img src="assets/dashboard/05_3d_studio.png"> | <img src="assets/dashboard/06_3d_library.png"> |
| **3D studio:** live competitor intelligence from the YouTube Data API steers topic choice. | **Generated library:** every 3D video with status and provenance. |

### Channel analytics and learning loop

<p align="center"><img src="assets/dashboard/07_analytics_daily.png" width="95%"></p>

| | |
|---|---|
| <img src="assets/dashboard/08_analytics_growth.png"> | <img src="assets/dashboard/09_analytics_learning.png"> |
| Growth, channel totals and best upload day. | What works by engine, format and category. This feeds back into topic ranking. |

---

## How it works

### End-to-end pipeline

```mermaid
flowchart LR
    subgraph D[1 · Discover]
        T1[Google Trends] --> R
        T2[News & Wikipedia] --> R
        T3[Reddit & Hacker News] --> R
        T4[Competitor channels<br/>YouTube Data API] --> R
        R[7-day Trend Radar<br/>clustering + LLM analyst]
    end
    subgraph S[2 · Research]
        R --> O{Official data?}
        O -- yes --> OD[SEC EDGAR · FAOSTAT<br/>OWID / World Bank]
        O -- no --> WT[Wikipedia stats tables]
        WT --> EV[Evidence-grounded<br/>LLM research]
    end
    subgraph Q[3 · Quality gates]
        OD --> MG[Motion gate<br/>overtakes · no frozen tail]
        EV --> MG
        MG --> FC[Multi-model fact-check<br/>Gemini + GPT-OSS + Wikipedia]
    end
    subgraph P[4 · Produce]
        FC --> RN[Renderer<br/>Short · Long · 3D]
        RN --> QA[Preview QA<br/>overlaps · hidden text]
        QA --> FF[FFmpeg encode<br/>+ synthesized audio]
        FF --> TH[Thumbnail designer]
        TH --> MD[SEO metadata]
    end
    subgraph U[5 · Publish & learn]
        MD --> YT[YouTube upload<br/>comment + playlist]
        YT --> AN[Analytics + Reporting API]
        AN -->|performance priors| R
    end
```

### System architecture

```mermaid
flowchart TB
    UI[Web dashboard<br/>Automation Center · 3D Studio · Analytics] --> ORC[Pipeline orchestrator]
    CRON[GitHub Actions / daily autopilot] --> ORC
    ORC --> INT[Intelligence layer<br/>trend engine · topic scoring · competitor radar]
    ORC --> DATA[Data layer<br/>official sources · Wikipedia tables · caching]
    ORC --> LLM[LLM gateway<br/>Groq + Gemini · shared token budget · fallbacks]
    ORC --> REN[Render engines<br/>bar-chart race · long-form story · 3D pillars]
    REN --> AUD[Audio engine<br/>music, whooshes, drum-rolls, boom]
    REN --> FFM[FFmpeg]
    ORC --> YTAPI[YouTube APIs<br/>Data · Analytics · Reporting]
    INT <--> DB[(SQLite<br/>production history · performance · research runs)]
    ORC <--> DB
    YTAPI --> DB
```

### Data-quality gate

Trust is the brand, so no video ships on invented numbers.

```mermaid
flowchart LR
    A[Candidate dataset] --> B{Motion check}
    B -- frozen / no overtakes --> X[Reject & blacklist topic<br/>→ discover another]
    B -- watchable race --> C{Fact-check}
    C --> C1[Gemini verifier]
    C --> C2[GPT-OSS-20B verifier]
    C --> C3[Wikipedia evidence scan]
    C1 & C2 & C3 --> D{Consensus within tolerance?}
    D -- no --> X
    D -- yes --> E[Render ✅]
    C -. APIs rate-limited .-> W[Pause, keep topic<br/>retry later]
```

### Self-learning loop

```mermaid
sequenceDiagram
    participant YT as YouTube
    participant P as Performance sync
    participant M as Performance model
    participant T as Trend Radar
    participant V as Video pipeline
    YT->>P: views, watch time, CTR, subscribed views
    P->>M: per-video scores (shrunk toward mean for small samples)
    M->>T: category / engine / format priors
    T->>V: re-ranked topic concepts
    V->>YT: new upload (tagged with engine + filter provenance)
```

---

## Engineering highlights

- **Custom 3D renderer in pure Python:** perspective projection, near-plane clipping, perspective texture warping with mip-maps, parallax layers, a camera on a monotone cubic spline (no jolts), billboarded labels and depth sorting.
- **Automated visual QA:** every render is checked frame by frame for overlapping or hidden text *before* encoding. Failing videos are never published, and a contact sheet shows exactly where the problem is.
- **LLM cost and rate-limit engineering:** a cross-process token-budget pool keeps free-tier Groq usage under its per-minute limits, with model fallbacks and Gemini key rotation.
- **No fabricated data:** projection and padding were removed entirely, official sources are used first, and a multi-verifier consensus check runs. Rejected topics are remembered so the system never retries them.
- **Retention-driven editing:** a spoiler-free opening hook, event cards for new #1 / surges / collapses (with a reason shown only when Wikipedia confirms it), seamless Short loops, and pacing that skips dead zones.
- **Synthesized sound design:** whooshes on overtakes, a drum-roll into the podium and a boom on the #1 reveal, all generated in code with no licensed audio.
- **Full provenance:** every video records which engine, filter and data source produced it, so analytics can attribute results to strategy.
- **Runs unattended:** a daily autopilot (local loop or GitHub Actions) syncs performance, refreshes trends and produces and publishes a batch.

<p align="center">
  <img src="assets/quality/automated_preview_qa_sheet.jpg" width="49%">
  <img src="assets/quality/3d_pillar_cards.png" width="30%">
</p>
<p align="center"><sub>Left: automated preview-QA contact sheet. Right: 3D pillar cards (logo + name plaque, fixed to the face).</sub></p>

---

## Tech stack

| Area | Tools |
|---|---|
| Language | Python 3.12 |
| Rendering | Pillow, NumPy (custom 2D/3D engines), FFmpeg (H.264, AAC) |
| AI | Groq (GPT-OSS-120B / 20B), Google Gemini, ONNX Runtime (U²-Net-P background removal) |
| Data | SEC EDGAR XBRL, FAOSTAT bulk, Our World in Data, World Bank, Wikipedia / MediaWiki API, Google Trends, RSS |
| Platform | YouTube Data API v3, YouTube Analytics API, YouTube Reporting API, OAuth 2.0 |
| Storage | SQLite, JSON caches |
| Ops | GitHub Actions (scheduled autopilot), local web dashboard |

---

## Contact

Interested in the project or a similar automation for your channel or brand? Get in touch and I'll be happy to give a live demo.
