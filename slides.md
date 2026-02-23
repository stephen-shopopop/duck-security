---
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: assets/cover-slidev.jpg
# some information about your slides (markdown enabled)
title: Welcome to duck security slides
titleTemplate: '%s - Duck Security'
info: |
  ## Duck Security slides
  Presentation slides for all people.
author: stephen deletang
keywords: security
presenter: true
browserExporter: build
download: true,
exportFilename: ducker-security-exported
export:
  format: pdf
  timeout: 30000
  dark: false
  withClicks: false
  withToc: false
twoslash: true
selectable: true
record: dev
contextMenu: true
wakelock: true
overviewSnapshots: false
colorSchema: auto
routerMode: history
aspectRation: 16/9
canvasWidth: 980
themeConfig:
  primary: '#5d8392'
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Duck security

Presentation slides for all people.

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/stephen-shopopop/duck-security" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
layout: center
title: présentation
class: px-14
---

<div class="w-full max-w-3xl mx-auto rounded-2xl border border-white/25 bg-white/10 backdrop-blur p-8 text-left shadow-xl">
  <p class="text-sm uppercase tracking-widest opacity-70 mb-2">Qui suis-je ?</p>
  <h2 class="text-4xl font-bold leading-tight mb-2">Stephen Deletang</h2>
  <p class="text-xl opacity-90 mb-5">Développeur back-end senior depuis plus de 10 ans</p>
  <p class="text-lg leading-relaxed opacity-90">
    Je crée des solutions logicielles sécurisées sur le cloud, simples et fiables pour tous.
  </p>
  <div class="mt-4 inline-flex items-center gap-3 rounded-xl border border-white/30 bg-white/10 px-3 py-2">
    <span class="text-sm opacity-80">Entreprises :</span>
    <span class="inline-flex items-center rounded-md px-2 py-1" style="background-color: #009fe3;">
      <img src="/assets/logos/epsa-energy.png" alt="Logo EPSA Energy" class="h-7 w-auto" />
    </span>
    <span class="inline-flex items-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/shopopop.png" alt="Logo Shopopop" class="h-7 w-auto" />
    </span>
    <span class="inline-flex items-center rounded-md px-2 py-1" style="background-color: #009fe3;">
      <img src="/assets/logos/e-dentic.webp" alt="Logo e-dentic" class="h-7 w-auto" />
    </span>
  </div>
  <div class="mt-3 flex flex-wrap items-center gap-1 rounded-xl border border-white/30 bg-white/10 px-3 py-2">
    <span class="text-sm opacity-80">Technologie :</span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/nodejs.svg" alt="Logo Node.js" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/golang.png" alt="Logo Golang" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/postgresql.svg" alt="Logo PostgreSQL" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/elasticsearch.svg" alt="Logo Elasticsearch" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/clickhouse.svg" alt="Logo ClickHouse" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/rabbitmq.svg" alt="Logo RabbitMQ" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/mqtt.svg" alt="Logo MQTT" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/mysql.svg" alt="Logo MySQL" class="h-7 w-24 object-contain" />
    </span>
    <span class="inline-flex w-28 items-center justify-center rounded-md bg-white px-2 py-1">
      <img src="/assets/logos/sqlite.svg" alt="Logo SQLite" class="h-7 w-24 object-contain" />
contain" />
    </span>
  </div>
  <div class="mt-6 flex flex-wrap gap-2 text-sm">
    <span class="px-3 py-1 rounded-full border border-white/30 bg-white/10">Sécurité</span>
    <span class="px-3 py-1 rounded-full border border-white/30 bg-white/10">Cloud</span>
    <span class="px-3 py-1 rounded-full border border-white/30 bg-white/10">Fiabilité</span>
    <span class="px-3 py-1 rounded-full border border-white/30 bg-white/10">Données</span>
    <span class="px-3 py-1 rounded-full border border-white/30 bg-white/10">Performance</span>
  </div>
</div>

---
src: ./pages/sommaire.md
---

---
src: ./pages/internet.md
---

---
src: ./pages/computer.md
---

---
src: ./pages/tiers-confiance.md
---

---
src: ./pages/pirates.md
---

---
src: ./pages/plus-loin.md
---

---
src: ./pages/questions.md
---

---
src: ./pages/remerciements.md
---

---
layout: end
---
