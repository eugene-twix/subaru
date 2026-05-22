# Subaru Impreza Landing — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Собрать single-page editorial-лендинг про Subaru Impreza — визуальное эссе о том, во что машина может превратиться (engine swap, тюнинг, неон, экстерьер). Не каталог услуг, а художественный нарратив. Главный цвет — розовый, эстетика — японская, премиум-планка — Porsche/Lexus.

**Architecture:** 3 параллельных дизайн-прототипа в `prototypes/` (vanilla HTML + CSS + минимум JS, без сборки). Пользователь выбирает один; финальный сайт собирается на его основе. Контент идентичен у всех трёх, разнится только подача. Все ассеты — CSS/SVG (фотографий машины нет на этапе прототипа).

**Tech Stack:**
- HTML5 + CSS3 (custom properties, grid, transforms, mix-blend-mode, backdrop-filter)
- Vanilla JS (Intersection Observer для scroll-reveal)
- Google Fonts (по концепции)
- SVG для силуэта машины, иероглифов, лепестков, dyno-графиков
- Без bundler, без React, без зависимостей

---

## 1. Контент (общий для всех концепций)

Тексты — русские, технические коды — латиница. Powered by research (см. источники в конце).

### 1.1 Hero
- Машина крупно, минимум текста, навигация: `История`, `Двигатель`, `Стейдж`, `Свет`, `Облик`
- Хедер ровно один — без CTA-кнопок

### 1.2 История / Философия
- 1–2 короткие колонки прозы. Тезис: «это не тюнинг, это становление характера»
- Декоративные акценты (вертикальные иероглифы / sumi-e мазок / манга-панели — по концепции)

### 1.3 Engine Swap
Четыре варианта, каждый с кодом, мощностью (стоковой), коротким нарративным описанием:

| Код | Источник | Стоковая мощность | Описание |
|---|---|---|---|
| `EJ257` | STI 2004+ | ~305 л.с. | Прямой путь к STI-характеру: forged internals, dual AVCS, larger intercooler |
| `EJ255` | WRX 2006+ | ~227 л.с. | Уличный баланс, closed-deck блок, VF39 турбина |
| `FA20DIT` | WRX 2015+ | ~268 л.с. | Современная инжекторная логика, direct injection |
| `2JZ-GTE` | Toyota Supra | ~280 л.с. (легендарно тюнингуемый до 1000+) | Красивая ересь — кроссовер культур |

**Note:** GD/GG/GE/GH шасси принимают EJ-семейство с минимальной кастомизацией. GR (2008+) сложнее — два CAN-bus, нужны ECU + ABS + steering angle + DCCD module.

### 1.4 Tuning Stages

| Стейдж | Что входит | Мощность |
|---|---|---|
| Stage 1 | ECU remap, intake, downpipe (cat-back), 95-100 RON | 260–300 л.с. |
| Stage 2 | + sports cat downpipe, 3-port BCS, бо́льший интеркулер | 320–380 л.с. |
| Stage 3+ | + новая турбина (VF35/VF39), forged internals, кованая поршневая | 400–500+ л.с. |

### 1.5 Underglow / Neon
- Виды: LED RGB полосы (наиболее популярны, IP67, RGB-IC), неоновые трубки (классика, фиксированный цвет)
- Зоны: подсветка днища (underglow), салон (footwell, dashboard), engine bay
- Контрольный комментарий о легальности: в РФ ПДД п.3.6 ограничивает световые приборы спереди (белый/жёлтый) и сзади (красный); цветной underglow — только на закрытых площадках/треке. Это упоминаем без морализаторства, как часть культуры.

### 1.6 Exterior
- Покраска: жемчуг розовый, чёрная вишня, перламутр с pink-kanji графикой
- Винил: матовый белый с pink brushstroke, сакура-стикеры, abstract liveries
- Кузов: carbon hood, widebody arches, ducktail spoiler, lip kit
- Диски: кованые (Volk TE37, Work, Enkei), bronze/white/black
- Оптика: smoked headlights, LED DRL

### 1.7 Closing Manifesto
- Короткий поэтический текст на тёмном/чистом фоне (по концепции). Машина в финальной форме.

---

## 2. Дизайн-концепции (от Codex)

### Концепция A — «Синдзюку 03:00»
**Vibe:** ночной токийский cyberpunk-editorial. Мокрый асфальт, pink underglow, вандинг-машины.

- **Palette:** primary `#FF2DAA`, deep black `#050507`, wet asphalt `#16171C`, cyan `#00E5FF`, signal red `#FF3B30`, soft white `#F5F1F4`, chrome `#A7AAB3`
- **Fonts:** Unbounded (headings) + Manrope (body) + IBM Plex Mono (tech labels)
- **Hero:** rear three-quarter, low-angle, под эстакадой, pink-glow на чёрной плёнке асфальта
- **Signature interaction:** «neon ignition scroll» — pink-линия пробегает по странице при скролле; engine heartbeat hover-пульсация
- **Grid:** 12-col, asymmetric, image-to-text 70/30
- **Risk:** не превратить в generic kanji-cyberpunk; держать chrome/cyan/white для дыхания

### Концепция B — «Лепесток и Сталь»
**Vibe:** тихий wabi-sabi premium-editorial. Сакура, sumi-e, ритуал.

- **Palette:** primary `#F58BB6`, ink black `#111111`, warm paper `#F6F0E8`, soft gray `#D8D2CA`, deep plum `#3A1828`, muted steel `#777B80`, sakura shadow `#E7B6C9`
- **Fonts:** Cormorant Garamond (headings) + IBM Plex Sans (body) + IBM Plex Mono (specs)
- **Hero:** side profile в студийном свете, дрейфующие лепестки, типографика плывёт над машиной
- **Signature interaction:** sumi-e ink-reveal масками; petal spec markers на hover
- **Grid:** 8-col, wide margins, image-to-text 60/40
- **Risk:** не скатиться в beige lifestyle-минимализм; розовый — дисциплинированный, не сладкий

### Концепция C — «Акихабара Pink Spec»
**Vibe:** itasha + 90s JDM magazine cover + arcade UI + vapor-wave. Громкий, но дисциплинированный.

- **Palette:** primary `#FF4FD8`, candy coral `#FF6B8A`, arcade blue `#4DDCFF`, deep violet `#2B123F`, off-white `#FFF7F2`, graphite `#18151E`, acid lime `#C9FF3D`
- **Fonts:** Russo One (headings) + Inter (body) + JetBrains Mono (UI labels)
- **Hero:** magazine-cover композиция, front three-quarter, sticker-overlays
- **Signature interaction:** spec-unlock scroll (плашки `ДВИГАТЕЛЬ ОТКРЫТ`, `СВЕТ АКТИВИРОВАН`); sticker hover system
- **Grid:** 12-col, modular magazine blocks, image-to-text 65/35
- **Risk:** не использовать copyright anime; не превратить в дешёвый tuner flyer

---

## 3. Файлы прототипов

```
prototypes/
├── index.html                          # лендер прототипов (3 карточки → 3 концепции)
├── 01-shinjuku-0300.html               # концепция A
├── 02-petal-and-steel.html             # концепция B
└── 03-akihabara-pink-spec.html         # концепция C
```

Каждый прототип — самодостаточный single-file HTML (CSS + JS inline). Открывается через `open prototypes/01-shinjuku-0300.html` или dev server `python3 -m http.server 5001`.

### 3.1 Общая структура прототипа

```html
<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Impreza — {Концепция}</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family={...}" rel="stylesheet">
  <style>/* design tokens, grid, sections */</style>
</head>
<body>
  <nav>{minimal nav, по концепции}</nav>
  <section class="hero">...</section>
  <section class="story">...</section>
  <section class="engine">...</section>
  <section class="stages">...</section>
  <section class="neon">...</section>
  <section class="exterior">...</section>
  <section class="manifesto">...</section>
  <footer>{минимальный}</footer>
  <script>/* IntersectionObserver reveal */</script>
</body>
</html>
```

### 3.2 SVG-арт вместо фото

Поскольку реальных фото нет, рисуем:
- **Силуэт Impreza** — упрощённый SVG в стиле side-profile (бампер, крыша, арки, спойлер). Один и тот же базовый SVG, но в каждой концепции стилизуется (neon outline / ink brush / sticker overlay)
- **Engine block** — schematic боксер-четвёрки (4 цилиндра горизонтально оппозитно)
- **Сакура-лепестки** — простые SVG-path, анимируются через CSS
- **Dyno curves** — SVG-path с stroke-dashoffset анимацией
- **Иероглифы** — Unicode (`力`, `速`, `光`, `桜`), в качестве декоративных акцентов (с дисциплиной)

---

## 4. Что НЕ делаем в прототипах

- Реальные фотографии (нет на этапе прототипа — заменяются на CSS/SVG)
- Видео и тяжёлые анимации (только лёгкие CSS-transitions + IntersectionObserver)
- Контактные формы, CTA «заказать», цены, ссылки на тюнинг-ателье
- I18n / язык-свитчер (только русский по требованию)
- Build pipeline, frameworks, CMS
- Реальные ссылки на auto.ru/IWiti/etc — фигурируют только как research-источники в комментариях

---

## 5. Acceptance criteria

- 3 прототипа открываются как статические HTML без ошибок в консоли
- Каждый прототип содержит все 7 секций (hero, history, engine, stages, neon, exterior, manifesto)
- На каждом — primary pink доминирует, типографика и palette строго по концепции
- `prototypes/index.html` — карточки-превью со ссылками на прототипы
- Responsive: разумно работает на 360px и 1440px (без mobile-first перфекционизма — это демо)
- Open Graph meta для красивого превью при шаринге

---

## 6. Roadmap

Сложность каждой задачи в относительных единицах (S/M/L), без часов.

| # | Задача | Сложность | Зависит от |
|---|---|---|---|
| 1 | Написать общий контент (тексты секций) | S | — |
| 2 | Нарисовать базовые SVG (силуэт, движок, лепестки, dyno) | M | — |
| 3 | Концепция A: `01-shinjuku-0300.html` | L | 1, 2 |
| 4 | Концепция B: `02-petal-and-steel.html` | L | 1, 2 |
| 5 | Концепция C: `03-akihabara-pink-spec.html` | L | 1, 2 |
| 6 | `prototypes/index.html` — выбор концепции | S | 3, 4, 5 |
| 7 | Сверка: открыть в Chrome, проверить нет ошибок, скриншоты hero-секций | S | 3, 4, 5 |

Задачи 3, 4, 5 — независимы и могут идти параллельно.

---

## 7. Open questions

- **Финальный выбор концепции:** будем ли мы после прототипов фиксировать одну и доводить до production, или развивать несколько параллельно?
- **Источник фото машины:** на каком этапе появятся реальные фотографии Impreza? Render? Студия? Стоковые?
- **Деплой:** локальный preview или нужен хостинг (GitHub Pages / Netlify)?

---

## 8. Research sources

### Engine swap
- [Easy Subaru Swap Engine Choices — iWire](https://iwireusa.com/blogs/iwire-university/easy-subaru-swap-engine-choices)
- [Subaru Engine Swap Compatibility Chart](https://engineoiljournal.com/subaru-engine-swap-compatibility-chart/)
- [EJ257 STI swap discussions — rs25.com](https://www.rs25.com/threads/suggestions-for-swapping-ej257-into-gc8.77970/)

### Tuning stages
- [Typical Upgrade Path — Newage 2.0 WRX — RaceDynamix](https://racedynamix.co.uk/remap/subaru-remapping/typical-upgrade-path-newage-2-0-wrx/)
- [Impreza WRX/STI Tuning Guide — ScoobyParts](https://scoobyparts.com/blog/ecu-remapping-tuning-the-subaru-impreza-wrx-and-sti/)
- [Subaru Impreza GC8 Tuning Guide — Fast Car](https://www.fastcar.co.uk/tuning-tech-guides/subaru-impreza-sti-tuning-guide/)
- [02-14 WRX Stage 1 Tune — Delicious Tuning](https://www.delicioustuning.com/node/503)

### Underglow / neon
- [Automotive LED Lighting Laws — Lighting Trendz](https://lightingtrendz.com/pages/automotive-led-lighting-laws-by-state-2025-guide)
- [LED and Neon Underglow Legal Considerations — CarUnderglowLaw](https://carunderglowlaw.com/led-and-neon-underglow-legal-considerations/)

### Design references
- [Lexus / premium scroll patterns — a-fresh](https://a-fresh.website/blog/10-best-automotive-website-examples-2025)
- [Animated landing page examples — SVGator](https://www.svgator.com/blog/animated-landing-pages-examples/)
- [Scrolling patterns — UXPin](https://www.uxpin.com/studio/blog/4-types-creative-website-scrolling-patterns/)
