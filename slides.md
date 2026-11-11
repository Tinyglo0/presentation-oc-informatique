---
# try also 'default' to start simple
theme: default
# some information about your slides (markdown enabled)
title: Option Informatique — Programme OC
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: "!px-10 !py-6"
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: false
# duration of the presentation
duration: 35min
colorSchema: light
layout: default
---

<div class="h-full flex flex-col justify-between">
<div>
  <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider bg-slate-100 text-slate-600 border border-slate-200 mb-3">
    <carbon:education class="text-sm text-[#0E9AA7]" /> Option Complémentaire
  </div>
  <h1 class="text-5xl font-black tracking-tight text-[#14213D] !m-0 !mb-2">
    OPTION <span class="text-transparent bg-clip-text bg-gradient-to-r from-[#0E9AA7] via-[#0E9AA7] to-[#F28C28]">INFORMATIQUE</span>
  </h1>
  <div class="text-lg font-semibold text-slate-500 flex items-center gap-2">
    <span>Programme OC Informatique</span>
    <span class="text-slate-300">·</span>
    <span class="text-[#0E9AA7] font-bold">M. Saudemont</span>
    <span class="text-slate-400">&amp;</span>
    <span class="text-[#F28C28] font-bold">M. Vasseur</span>
  </div>
</div>

<div class="p-4 rounded-2xl bg-gradient-to-r from-[#EEF6F8] via-white to-[#FFF4E8] border border-slate-200 shadow-xs">
  <div class="text-base leading-snug text-[#14213D] font-bold mb-1.5">
    « <span class="text-[#0E9AA7]">De la donnée brute</span> à votre propre <span class="text-[#F28C28]">application ou jeu vidéo</span>, en une année. »
  </div>
  <div class="text-xs text-slate-600 leading-relaxed">
    Vous découvrirez comment stocker et interroger des millions d’informations, comment il est possible de coder à plusieurs sans se marcher dessus, puis comment on transforme tout cela en un programme que n’importe qui peut utiliser.
  </div>
</div>

<div>
  <div class="text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-2">
    Cliquez sur une étape pour explorer le programme :
  </div>
  <div class="grid grid-cols-5 gap-2.5">
    <div @click="$slidev.nav.go(3)" class="p-2.5 rounded-xl bg-[#EEF6F8] border border-[#0E9AA7]/30 hover:border-[#0E9AA7] text-center cursor-pointer transition-transform hover:-translate-y-0.5">
      <div class="text-[#0E9AA7] font-bold text-xs">1. Données &amp; SQL</div>
      <div class="text-[10px] text-slate-500 mt-0.5">interroger l'info</div>
    </div>
    <div @click="$slidev.nav.go(4)" class="p-2.5 rounded-xl bg-[#EEF6F8] border border-[#0E9AA7]/30 hover:border-[#0E9AA7] text-center cursor-pointer transition-transform hover:-translate-y-0.5">
      <div class="text-[#0E9AA7] font-bold text-xs">2. Git</div>
      <div class="text-[10px] text-slate-500 mt-0.5">travailler à plusieurs</div>
    </div>
    <div @click="$slidev.nav.go(5)" class="p-2.5 rounded-xl bg-[#EEF6F8] border border-[#0E9AA7]/30 hover:border-[#0E9AA7] text-center cursor-pointer transition-transform hover:-translate-y-0.5">
      <div class="text-[#0E9AA7] font-bold text-xs">3. Site Web</div>
      <div class="text-[10px] text-slate-500 mt-0.5">HTML / CSS</div>
    </div>
    <div @click="$slidev.nav.go(6)" class="p-2.5 rounded-xl bg-[#FFF4E8] border border-[#F28C28]/30 hover:border-[#F28C28] text-center cursor-pointer transition-transform hover:-translate-y-0.5">
      <div class="text-[#F28C28] font-bold text-xs">4. Objets</div>
      <div class="text-[10px] text-slate-500 mt-0.5">Python orienté objet</div>
    </div>
    <div @click="$slidev.nav.go(7)" class="p-2.5 rounded-xl bg-[#FFF4E8] border border-[#F28C28]/30 hover:border-[#F28C28] text-center cursor-pointer transition-transform hover:-translate-y-0.5">
      <div class="text-[#F28C28] font-bold text-xs">5. Interface &amp; Jeu</div>
      <div class="text-[10px] text-slate-500 mt-0.5">Tkinter ou Pygame</div>
    </div>
  </div>
</div>

<div class="flex justify-between items-center text-[11px] text-slate-400 pt-2 border-t border-slate-100">
  <span><strong class="text-[#0E9AA7]">Semestre 1 :</strong> Ce qui se cache derrière l’écran</span>
  <span><strong class="text-[#F28C28]">Semestre 2 :</strong> Donner vie à une application</span>
</div>
</div>

<!--
Présentation générale de l'option informatique devant les élèves. Mettre l'accent sur l'accessibilité et la progression sur l'année.
-->

---
class: "!px-10 !py-5"
layout: default
title: Le parcours d'une année
---

<div class="h-full flex flex-col justify-between">
<div>
  <h2 class="text-3xl font-extrabold text-[#14213D] !m-0 !mb-1">
    Le parcours d'une année
  </h2>
  <div class="text-xs text-slate-500 font-medium">
    De la donnée brute à votre propre application ou jeu vidéo : une progression continue sur deux semestres.
  </div>
</div>

<div class="p-3 bg-white rounded-xl border border-slate-200 shadow-xs flex justify-center items-center">
  <img src="/timeline.svg" class="w-full max-h-46 object-contain" alt="Frise chronologique OC Info" />
</div>

<div class="grid grid-cols-2 gap-5">
  <div v-click class="p-4 rounded-xl bg-white border border-slate-200/90 shadow-xs flex flex-col justify-between">
    <div>
      <div class="flex items-center justify-between mb-2">
        <span class="inline-flex items-center gap-1.5 px-2 py-0.5 rounded-md text-[11px] font-semibold bg-[#0E9AA7]/10 text-[#0E9AA7] border border-[#0E9AA7]/20">
          <span class="w-1.5 h-1.5 rounded-full bg-[#0E9AA7]"></span>
          Semestre 1
        </span>
        <span class="text-xs text-slate-500 font-medium">M. Saudemont</span>
      </div>
      <div class="text-sm font-bold text-[#14213D] mb-1.5">
        Ce qui se cache derrière l’écran
      </div>
      <div class="text-xs text-slate-600 leading-relaxed">
        Derrière chaque appli, chaque réseau social, chaque plateforme de streaming : des données (<span class="font-semibold text-slate-800">SQL</span>), de la collaboration (<span class="font-semibold text-slate-800">Git</span>) et du code web (<span class="font-semibold text-slate-800">HTML/CSS</span>).
      </div>
    </div>
  </div>

  <div v-click class="p-4 rounded-xl bg-white border border-slate-200/90 shadow-xs flex flex-col justify-between">
    <div>
      <div class="flex items-center justify-between mb-2">
        <span class="inline-flex items-center gap-1.5 px-2 py-0.5 rounded-md text-[11px] font-semibold bg-[#F28C28]/10 text-[#F28C28] border border-[#F28C28]/25">
          <span class="w-1.5 h-1.5 rounded-full bg-[#F28C28]"></span>
          Semestre 2
        </span>
        <span class="text-xs text-slate-500 font-medium">M. Vasseur</span>
      </div>
      <div class="text-sm font-bold text-[#14213D] mb-1.5">
        Donner vie à une application
      </div>
      <div class="text-xs text-slate-600 leading-relaxed">
        Tout ce que vous aurez appris tourne en coulisses. On construit l'architecture en <span class="font-semibold text-slate-800">Python orienté objet</span> et l'interface (<span class="font-semibold text-slate-800">Tkinter</span> ou <span class="font-semibold text-slate-800">Pygame</span>) en <span class="font-semibold text-slate-800">projet en duo</span>.
      </div>
    </div>
  </div>
</div>
</div>

<!--
Faire un tour d'horizon des deux semestres. Montrer la cohérence globale du cursus.
-->

---
class: "!px-10 !py-5"
layout: default
title: Données & SQL
---

<div class="h-full flex flex-col justify-start gap-10">
<div>
  <div class="flex items-center justify-between border-b border-slate-200 pb-1.5 mb-2">
    <div class="flex items-center gap-2.5">
      <span class="px-2.5 py-0.5 rounded-md text-[11px] font-bold uppercase tracking-wider bg-[#0E9AA7] text-white">Semestre 1</span>
      <span class="text-xs text-slate-500 font-semibold italic">Ce qui se cache derrière l’écran · avec M. Saudemont</span>
    </div>
    <span class="text-xs font-mono font-bold text-[#0E9AA7]">Étape 1 / 5</span>
  </div>
  <h2 class="text-2xl font-extrabold text-[#14213D] !m-0 !mb-1">
    Données &amp; SQL : interroger l’information
  </h2>
  <div class="text-xs text-slate-600">
    « Partez d’un simple fichier <code>.csv</code> et apprenez à interroger de grandes quantités d’informations avec SQL, le langage universel des bases de données. »
  </div>
</div>

<SqlDemo />
</div>

<!--
Expliquer aux élèves l'intérêt de SQL : toute application (Netflix, Instagram, banques) repose sur une base relationnelle.
-->

---
class: "!px-10 !py-5"
layout: default
title: Git & Collaboration
---

<div class="h-full flex flex-col justify-start gap-10">
<div>
  <div class="flex items-center justify-between border-b border-slate-200 pb-1.5 mb-2">
    <div class="flex items-center gap-2.5">
      <span class="px-2.5 py-0.5 rounded-md text-[11px] font-bold uppercase tracking-wider bg-[#0E9AA7] text-white">Semestre 1</span>
      <span class="text-xs text-slate-500 font-semibold italic">Ce qui se cache derrière l’écran · avec M. Saudemont</span>
    </div>
    <span class="text-xs font-mono font-bold text-[#0E9AA7]">Étape 2 / 5</span>
  </div>
  <h2 class="text-2xl font-extrabold text-[#14213D] !m-0 !mb-1">
    Git : travailler à plusieurs sans se marcher dessus
  </h2>
  <div class="text-xs text-slate-600 mb-2">
    « Comment plusieurs développeurs travaillent-ils sur le même projet sans effacer le travail des autres ? Historique, branches, collaboration : l’outil des pros. »
  </div>
</div>

<GitDemo />
</div>

<!--
Montrer comment Git est indispensable dès qu'on travaille à deux ou en équipe. C'est une compétence clé pour l'université et le monde pro.
-->

---
class: "!px-10 !py-5"
layout: default
title: Site Web HTML/CSS
---

<div class="h-full flex flex-col justify-start gap-10">
<div>
  <div class="flex items-center justify-between border-b border-slate-200 pb-1.5 mb-2">
    <div class="flex items-center gap-2.5">
      <span class="px-2.5 py-0.5 rounded-md text-[11px] font-bold uppercase tracking-wider bg-[#0E9AA7] text-white">Semestre 1</span>
      <span class="text-xs text-slate-500 font-semibold italic">Ce qui se cache derrière l’écran · avec M. Saudemont</span>
    </div>
    <span class="text-xs font-mono font-bold text-[#0E9AA7]">Étape 3 / 5</span>
  </div>
  <h2 class="text-2xl font-extrabold text-[#14213D] !m-0 !mb-1">
    Site web statique : HTML &amp; CSS
  </h2>
  <div class="text-xs text-slate-600 mb-2">
    « Créez votre propre site de A à Z en HTML/CSS, là où logique, structure et design se rencontrent. »
  </div>
</div>

<WebDemo />
</div>

<!--
Mettre en valeur le plaisir visuel immédiat : les élèves voient tout de suite ce qu'ils créent dans le navigateur.
-->

---
class: "!px-10 !py-5"
layout: default
title: Python avancé & Objets
---

<div class="h-full flex flex-col justify-between">
<div>
  <div class="flex items-center justify-between border-b border-slate-200 pb-1.5 mb-2">
    <div class="flex items-center gap-2.5">
      <span class="px-2.5 py-0.5 rounded-md text-[11px] font-bold uppercase tracking-wider bg-[#F28C28] text-white">Semestre 2</span>
      <span class="text-xs text-slate-500 font-semibold italic">Donner vie à une application · avec M. Vasseur</span>
    </div>
    <span class="text-xs font-mono font-bold text-[#F28C28]">Étape 4 / 5</span>
  </div>
  <h2 class="text-2xl font-extrabold text-[#14213D] !m-0 !mb-1">
    Python avancé &amp; Programmation Orientée Objet
  </h2>
  <div class="text-xs text-slate-600 mb-2">
    « Dictionnaires, puis programmation orientée objet : une application, ce n’est plus une recette de cuisine mais des objets qui interagissent. »
  </div>
</div>

<PooDemo />
</div>

<!--
La POO est la pierre angulaire de l'informatique moderne (Java, C++, C#, Python, TypeScript). C'est un atout gigantesque pour les études supérieures.
-->

---
class: "!px-10 !py-5"
layout: default
title: Interfaces & Jeux
---

<div class="h-full flex flex-col justify-start gap-6">
<div>
  <div class="flex items-center justify-between border-b border-slate-200 pb-1.5 mb-2">
    <div class="flex items-center gap-2.5">
      <span class="px-2.5 py-0.5 rounded-md text-[11px] font-bold uppercase tracking-wider bg-[#F28C28] text-white">Semestre 2</span>
      <span class="text-xs text-slate-500 font-semibold italic">Donner vie à une application · avec M. Vasseur</span>
    </div>
    <span class="text-xs font-mono font-bold text-[#F28C28]">Étape 5 / 5</span>
  </div>
  <h2 class="text-2xl font-extrabold text-[#14213D] !m-0 !mb-1">
    Interface graphique : logiciel ou jeu vidéo, au choix !
  </h2>
  <div class="text-xs text-slate-600 mb-2">
    « Tout ce que vous aurez appris tourne en coulisses. Il manque une interface pour que ça devienne une vraie application : on la construit. »
  </div>
</div>

<GuiDemo />
</div>

<!--
Souligner que chaque groupe est libre de son sujet : utilitaire ou jeu vidéo selon les envies des élèves.
-->

---
layout: default
class: "!px-10 !py-5"
title: Projet en duo & Conclusion
---

<div class="h-full flex flex-col justify-between">
  <div class="text-center">
    <div class="inline-flex items-center gap-2 px-3 py-0.5 rounded-full bg-[#14213D] text-white text-[11px] font-bold tracking-widest uppercase mb-1.5">
      Conclusion
    </div>
    <h1 class="!text-2xl font-extrabold text-[#14213D] !m-0">Pourquoi choisir l'OC Informatique ?</h1>
    <div class="text-slate-500 text-xs mt-1">Bien plus que du code : une boîte à outils complète pour vos études et projets</div>
  </div>
<div class="grid grid-cols-3 gap-4 my-2.5">
  <div v-click class="bg-white rounded-xl p-4 border border-slate-200/90 shadow-xs flex flex-col justify-between">
    <div>
      <span class="inline-flex items-center gap-1.5 px-2 py-0.5 rounded-md text-[11px] font-semibold bg-[#0E9AA7]/10 text-[#0E9AA7] border border-[#0E9AA7]/20">
        <span class="w-1.5 h-1.5 rounded-full bg-[#0E9AA7]"></span>
        01
      </span>
      <h3 class="font-bold text-[#14213D] text-sm mt-2 mb-1.5">Créer de A à Z</h3>
      <div class="text-xs text-slate-600 leading-relaxed">
        Sortir de la console pour concevoir de <span class="font-semibold text-slate-800">vraies applications</span> : sites web interactifs, bases de données, jeux 2D et logiciels graphiques.
      </div>
    </div>
    <div class="mt-3 pt-2 border-t border-slate-100 text-xs font-semibold text-[#0E9AA7] flex items-center gap-1.5">
      <span class="w-1 h-1 rounded-full bg-[#0E9AA7]"></span>
      Autonomie &amp; Créativité
    </div>
  </div>

  <div v-click class="bg-white rounded-xl p-4 border border-slate-200/90 shadow-xs flex flex-col justify-between">
    <div>
      <span class="inline-flex items-center gap-1.5 px-2 py-0.5 rounded-md text-[11px] font-semibold bg-slate-100 text-[#14213D] border border-slate-200">
        <span class="w-1.5 h-1.5 rounded-full bg-[#14213D]"></span>
        02
      </span>
      <h3 class="font-bold text-[#14213D] text-sm mt-2 mb-1.5">Travailler comme les pros</h3>
      <div class="text-xs text-slate-600 leading-relaxed">
        Maîtriser les outils standards de l'industrie et des hautes écoles (<span class="font-semibold text-slate-800">Git, SQL, architecture POO</span>) pour collaborer efficacement en équipe.
      </div>
    </div>
    <div class="mt-3 pt-2 border-t border-slate-100 text-xs font-semibold text-[#14213D] flex items-center gap-1.5">
      <span class="w-1 h-1 rounded-full bg-[#14213D]"></span>
      Méthode &amp; Rigueur
    </div>
  </div>

  <div v-click class="bg-white rounded-xl p-4 border border-slate-200/90 shadow-xs flex flex-col justify-between">
    <div>
      <span class="inline-flex items-center gap-1.5 px-2 py-0.5 rounded-md text-[11px] font-semibold bg-[#F28C28]/10 text-[#F28C28] border border-[#F28C28]/25">
        <span class="w-1.5 h-1.5 rounded-full bg-[#F28C28]"></span>
        03
      </span>
      <h3 class="font-bold text-[#14213D] text-sm mt-2 mb-1.5">Un atout pour le supérieur</h3>
      <div class="text-xs text-slate-600 leading-relaxed">
        Idéal pour l'<span class="font-semibold text-slate-800">EPFL, l'UNIGE, les HES</span> ou toute filière scientifique, d'ingénierie, d'économie, de données ou de design numérique.
      </div>
    </div>
    <div class="mt-3 pt-2 border-t border-slate-100 text-xs font-semibold text-[#F28C28] flex items-center gap-1.5">
      <span class="w-1 h-1 rounded-full bg-[#F28C28]"></span>
      Longueur d'avance
    </div>
  </div>
</div>
  <div v-click class="bg-gradient-to-r from-[#14213D] via-[#1d3158] to-[#0E9AA7] rounded-xl p-4 text-white flex items-center justify-between shadow-lg">
    <div class="flex items-center gap-3">
      <div class="w-10 h-10 rounded-full bg-white/15 flex items-center justify-center">
        <lucide:rocket class="w-5 h-5 text-white" />
      </div>
      <div>
        <h3 class="text-base font-bold text-white !m-0">Des questions ?</h3>
        <div class="text-xs text-slate-200 mt-0.5">
          N'hésitez pas à en discuter avec <strong>M. Saudemont</strong> (Semestre 1) ou <strong>M. Vasseur</strong> (Semestre 2) !
        </div>
      </div>
    </div>
    <button @click="$slidev.nav.go(1)" class="px-3.5 py-2 rounded-lg bg-white text-[#14213D] font-bold text-xs shadow hover:bg-slate-100 transition cursor-pointer shrink-0 flex items-center gap-1.5">
      <lucide:rotate-ccw class="w-3.5 h-3.5" />
      <span>Revoir depuis le début</span>
    </button>
  </div>
</div>

<!--
Répondre aux questions des élèves sur l'organisation, le matériel, le niveau attendu (tous niveaux bienvenus).
-->
