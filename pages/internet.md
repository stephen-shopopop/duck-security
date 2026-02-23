---
title: Comment fonctionne Internet ?
layout: center
class: px-14
---

<div class="w-full max-w-3xl mx-auto rounded-2xl border border-white/25 bg-white/10 backdrop-blur p-10 text-center shadow-xl">
	<h1 class="text-4xl font-bold mb-6 flex items-center justify-center gap-3">🌐 Comment fonctionne Internet&nbsp;?</h1>
	<p class="text-xl opacity-90 mb-2">Un réseau mondial qui relie tout&nbsp;: ordinateurs, serveurs, objets connectés…</p>
</div>

---
layout: center
---

<div class="max-w-2xl mx-auto rounded-xl border border-white/20 bg-white/5 p-7 shadow-lg">
	<img src="../assets/internet-intro.gif" alt="Internet fun" class="mx-auto mb-4 rounded-xl shadow-md w-48" />
	<h2 class="text-2xl font-bold mb-3 flex items-center gap-2">🌍 Qu'est-ce qu'Internet&nbsp;?</h2>
	<ul class="text-lg leading-relaxed space-y-2 text-left">
		<li>🔗 Un réseau mondial d'ordinateurs connectés</li>
		<li>🌏 Permet l'échange d'informations partout dans le monde</li>
	</ul>
</div>

---
layout: center
---

<div class="max-w-2xl mx-auto rounded-xl border border-white/20 bg-white/5 p-7 shadow-lg">
	<img src="../assets/internet-composants.gif" alt="Composants clés fun" class="mx-auto mb-4 rounded-xl shadow-md w-48" />
	<h2 class="text-2xl font-bold mb-3 flex items-center gap-2">🧩 Les composants clés</h2>
	<ul class="text-lg leading-relaxed space-y-2 text-left">
		<li>💻 <b>Ordinateurs & appareils</b> : utilisateurs finaux</li>
		<li>📡 <b>Routeurs</b> : dirigent le trafic</li>
		<li>🗄️ <b>Serveurs</b> : stockent et fournissent des données</li>
		<li>🌐 <b>Fournisseurs d'accès (FAI)</b> : connectent les utilisateurs au réseau</li>
	</ul>
</div>

---
layout: center
---

<div class="max-w-2xl mx-auto rounded-xl border border-white/20 bg-white/5 p-7 shadow-lg">
	<img src="../assets/internet-circulation.gif" alt="Circulation information fun" class="mx-auto mb-4 rounded-xl shadow-md w-48" />
	<h2 class="text-2xl font-bold mb-3 flex items-center gap-2">🔄 Comment circule l'information&nbsp;?</h2>
	<ol class="list-decimal ml-6 text-lg leading-relaxed space-y-1 text-left">
		<li>L'utilisateur envoie une requête (ex&nbsp;: ouvrir un site web)</li>
		<li>La requête passe par le FAI et des routeurs</li>
		<li>Le serveur reçoit la requête et répond</li>
		<li>Les données reviennent à l'utilisateur</li>
	</ol>
</div>

---
layout: center
---

<div class="max-w-2xl mx-auto rounded-xl border border-white/20 bg-white/5 p-7 shadow-lg">
	<img src="../assets/internet-protocoles.gif" alt="Protocoles fun" class="mx-auto mb-4 rounded-xl shadow-md w-48" />
	<h2 class="text-2xl font-bold mb-3 flex items-center gap-2">📑 Protocoles essentiels</h2>
	<ul class="text-lg leading-relaxed space-y-2 text-left">
		<li>🛣️ <b>TCP/IP</b> : assure la transmission fiable des données</li>
		<li>🔒 <b>HTTP/HTTPS</b> : pour accéder aux sites web</li>
		<li>🔤 <b>DNS</b> : traduit les noms de domaine en adresses IP</li>
	</ul>
</div>

---
layout: center
---

<div class="max-w-2xl mx-auto rounded-xl border border-white/20 bg-white/5 p-7 shadow-lg">
	<img src="../assets/internet-resume.gif" alt="Résumé fun" class="mx-auto mb-4 rounded-xl shadow-md w-48" />
	<h2 class="text-2xl font-bold mb-3 flex items-center gap-2">📝 Résumé</h2>
	<ul class="text-lg leading-relaxed space-y-2 text-left">
		<li>🌐 Internet connecte des milliards d'appareils</li>
		<li>📑 Utilise des protocoles pour garantir la communication</li>
		<li>⚡ Permet l'accès rapide à l'information partout</li>
	</ul>
</div>

---
title: Schéma récapitulatif Internet
layout: center
---

<div class="max-w-3xl mx-auto rounded-xl border border-white/20 bg-white/5 p-8 shadow-lg">
  <h2 class="text-2xl font-bold mb-4 flex items-center gap-2">🗺️ Schéma récapitulatif</h2>
  <div class="w-full flex justify-center">

```mermaid {theme: 'neutral', scale: 0.7}
flowchart LR
  style A fill:#f9fafb,stroke:#2563eb,stroke-width:2px
  style B fill:#e0e7ff,stroke:#6366f1,stroke-width:2px
  style C fill:#f1f5f9,stroke:#0ea5e9,stroke-width:2px
  style D fill:#fef9c3,stroke:#f59e42,stroke-width:2px
  style E fill:#f3e8ff,stroke:#a21caf,stroke-width:2px
  style F fill:#f3e8ff,stroke:#a21caf,stroke-width:2px
  style G fill:#e0f2fe,stroke:#0369a1,stroke-width:2px
  style H fill:#f1f5f9,stroke:#0ea5e9,stroke-width:2px
  A([<b>Utilisateur<br/>Appareil</b>]) -->|Connexion| B([<b>FAI</b><br/><span style='font-size:0.8em'>Fournisseur d'accès</span>])
  B -->|Routage| C([<b>Routeurs</b>])
  C -->|Acheminement| D([<b>Serveur Web</b>])
  D -->|Réponse| C
  C -->|Retour| B
  B -->|Données| A
  D --> E([<b>Base de données</b>])
  D --> F([<b>Autres serveurs</b>])
  C -.-> G([<b>Internet</b>])
  G -.-> C
  B -.-> H([<b>DNS</b>])
  H -.-> B
```

  </div>
  <p class="text-lg opacity-80 mt-4">Ce schéma illustre les principaux composants et flux d'Internet&nbsp;: utilisateurs, FAI, routeurs, serveurs, protocoles…</p>
</div>
