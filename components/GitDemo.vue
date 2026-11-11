<script setup lang="ts">
import { ref } from 'vue'

const currentStep = ref(1)

interface GitCommit {
  hash: string
  branch: 'main' | 'combat'
  author: 'Bob' | 'Alice'
  msg: string
  step: number
}

const stepsMeta = [
  {
    step: 1,
    title: '1. Commit initial sur main',
    cli: '$ git commit -m "Init: structure du jeu"',
    explain: 'Alice et Bob démarrent le projet commun sur la branche principale.',
  },
  {
    step: 2,
    title: '2. Alice crée sa branche isolée',
    cli: '$ git checkout -b combat && git commit -m "PV"',
    explain: 'Alice s\'isole pour coder les combats. Bob avance sur le son en parallèle.',
  },
  {
    step: 3,
    title: '3. Alice termine sa fonctionnalité',
    cli: '$ git commit -m "feat: animation attaque"',
    explain: 'Alice commite ses animations. Le code de Bob reste 100% protégé.',
  },
  {
    step: 4,
    title: '4. Fusion finale sans conflit',
    cli: '$ git checkout main && git merge combat',
    explain: 'Git assemble automatiquement le combat d\'Alice et le son de Bob.',
  },
]
</script>

<template>
  <div class="grid grid-cols-12 gap-3.5 items-stretch text-xs min-w-0">
    <!-- COLONNE GAUCHE (4 cols) : Sans Git vs Avec Git -->
    <div class="col-span-4 flex flex-col justify-between space-y-2 min-w-0">
      <!-- Faux explorateur chaotique sans Git -->
      <div class="p-2.5 rounded-xl bg-red-50 border border-red-200 shadow-2xs">
        <div class="flex items-center justify-between font-bold text-red-800 text-[11px] mb-1">
          <div class="flex items-center gap-1.5">
            <span class="w-2 h-2 rounded-full bg-red-500"></span>
            <span>Sans Git (le cauchemar)</span>
          </div>
          <span class="text-[9px] font-mono text-red-500">Chaos</span>
        </div>
        <div class="font-mono text-[9px] text-red-900 bg-white/95 p-2 rounded-lg border border-red-200/80 space-y-0.8 shadow-inner">
          <div class="flex items-center justify-between opacity-60">
            <span class="flex items-center gap-1"><lucide:file-code class="w-3 h-3 text-red-400" /> jeu_v1.py</span>
            <span class="text-[8px] text-slate-400">14:00</span>
          </div>
          <div class="flex items-center justify-between opacity-75">
            <span class="flex items-center gap-1"><lucide:file-code class="w-3 h-3 text-red-400" /> jeu_v2_final.py</span>
            <span class="text-[8px] text-slate-400">18:30</span>
          </div>
          <div class="font-bold text-red-600 bg-red-100/80 px-1 py-0.5 rounded flex items-center gap-1">
            <lucide:file-warning class="w-3 h-3 text-red-600" />
            <span>jeu_FINAL_Alice(2).py</span>
          </div>
          <div class="text-[8.5px] text-red-500 italic pt-0.5">
            ↳ Le travail de Bob a été écrasé par mail !
          </div>
        </div>
      </div>

      <!-- Les 3 atouts de Git -->
      <div class="p-2.5 rounded-xl bg-[#EEF6F8] border border-[#0E9AA7]/30 flex-1 flex flex-col justify-between shadow-2xs">
        <div>
          <div class="flex items-center gap-1.5 font-bold text-[#0E9AA7] text-[11px] mb-1.5">
            <span class="w-2 h-2 rounded-full bg-[#0E9AA7]"></span>
            <span>L'esprit Git (l'outil des pros)</span>
          </div>
          <div class="space-y-1.5 text-slate-700 text-[10.5px]">
            <div class="flex items-center gap-2 bg-white/90 p-1.5 rounded-lg border border-[#0E9AA7]/20">
              <lucide:git-branch class="w-3.5 h-3.5 text-[#0E9AA7] shrink-0" />
              <div>
                <strong class="text-[#14213D]">Branches :</strong> deux pistes parallèles sans aucun risque d'écrasement.
              </div>
            </div>
            <div class="flex items-center gap-2 bg-white/90 p-1.5 rounded-lg border border-[#0E9AA7]/20">
              <lucide:git-commit-horizontal class="w-3.5 h-3.5 text-[#0E9AA7] shrink-0" />
              <div>
                <strong class="text-[#14213D]">Commits :</strong> chaque version est un point de retour dans le temps.
              </div>
            </div>
            <div class="flex items-center gap-2 bg-white/90 p-1.5 rounded-lg border border-[#0E9AA7]/20">
              <lucide:git-merge class="w-3.5 h-3.5 text-[#0E9AA7] shrink-0" />
              <div>
                <strong class="text-[#14213D]">Merge :</strong> fusion mathématique intelligente des travaux.
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- COLONNE DROITE (8 cols) : Git Graph aéré sans superposition -->
    <div class="col-span-8 p-3 rounded-xl bg-white border border-slate-200 shadow-xs flex flex-col justify-between space-y-2 min-w-0">
      <!-- En-tête avec contrôles pas-à-pas -->
      <div class="flex items-center justify-between">
        <div class="flex items-center gap-2">
          <span class="inline-flex items-center gap-1 px-2 py-0.5 rounded bg-slate-900 text-slate-200 font-mono text-[10px] font-bold">
            <span class="text-[#0E9AA7]">git</span> graph
          </span>
          <span class="text-slate-500 font-semibold text-[11px]">Visualiseur de branches</span>
        </div>
        <div class="flex gap-1 bg-slate-100 p-0.5 rounded-lg border border-slate-200">
          <button
            v-for="s in [1, 2, 3, 4]"
            :key="s"
            @click="currentStep = s"
            class="px-2.5 py-0.5 rounded-md font-bold text-[10.5px] cursor-pointer transition-all"
            :class="currentStep === s ? 'bg-[#0E9AA7] text-white shadow-xs' : 'text-slate-600 hover:text-[#0E9AA7]'"
          >
            Étape {{ s }}
          </button>
        </div>
      </div>

      <!-- VISUALISEUR GIT GRAPH SANS AUCUNE SUPERPOSITION -->
      <div class="relative bg-[#0F172A] rounded-xl border border-slate-800 p-2.5 overflow-hidden shadow-inner h-[140px]">
        <!-- Grille discrète en arrière-plan -->
        <div class="absolute inset-0 opacity-15 pointer-events-none bg-[radial-gradient(#38bdf8_1px,transparent_1px)] [background-size:16px_16px]"></div>

        <!-- ZONE 1 : BADGES DE LA BRANCHE ALICE (TOUT EN HAUT - Y: 6px à 28px) -->
        <div class="absolute top-2 left-3 right-3 z-10 flex items-center justify-between">
          <div class="flex items-center gap-1.5">
            <span class="px-2 py-0.5 rounded text-[9.5px] font-mono font-bold bg-[#F28C28] text-white shadow-xs inline-flex items-center gap-1">
              <lucide:git-branch class="w-2.5 h-2.5" />
              <span>combat</span>
            </span>
            <span class="text-slate-400 text-[10px] inline-flex items-center gap-1">
              <lucide:user class="w-3 h-3" />
              <span>Alice</span>
            </span>
          </div>

          <!-- Pointers de commits actifs d'Alice (au-dessus du rail, ne touche rien) -->
          <div class="flex items-center gap-1.5">
            <span
              v-if="currentStep === 2"
              class="px-1.5 py-0.2 rounded bg-[#F28C28]/20 border border-[#F28C28] text-[#F28C28] font-mono text-[9px] font-bold animate-pulse inline-flex items-center gap-1"
            >
              <lucide:heart class="w-2.5 h-2.5" />
              <span>PV [7c9a1]</span>
            </span>
            <span
              v-if="currentStep >= 3"
              class="px-1.5 py-0.2 rounded bg-[#F28C28]/20 border border-[#F28C28] text-[#F28C28] font-mono text-[9px] font-bold inline-flex items-center gap-1"
            >
              <lucide:swords class="w-2.5 h-2.5" />
              <span>Attaque [9e1c4]</span>
            </span>
            <span
              v-if="currentStep >= 4"
              class="px-1.5 py-0.2 rounded bg-emerald-500/20 border border-emerald-500 text-emerald-400 font-mono text-[9px] font-bold inline-flex items-center gap-1"
            >
              <lucide:check class="w-2.5 h-2.5" />
              <span>merged</span>
            </span>
          </div>
        </div>

        <!-- ZONE 2 : RAILS & CERCLES SVG PURS (AU MILIEU - Alice à Y=48, Bob à Y=94) -->
        <svg class="absolute inset-0 w-full h-full pointer-events-none" viewBox="0 0 500 140" preserveAspectRatio="none">
          <!-- Rail de la branche principale 'main' (Teal #0E9AA7) à Y = 94 -->
          <line
            x1="35"
            y1="94"
            :x2="currentStep === 1 ? 170 : currentStep <= 3 ? 300 : 455"
            y2="94"
            stroke="#0E9AA7"
            stroke-width="3"
            stroke-linecap="round"
          />

          <!-- Embranchement de 'combat' (Orange #F28C28) qui part de (140, 94) vers (220, 48) -->
          <path
            v-if="currentStep >= 2"
            :d="currentStep === 2
              ? 'M 140 94 C 170 94, 185 48, 220 48 L 250 48'
              : 'M 140 94 C 170 94, 185 48, 220 48 L 340 48'"
            fill="none"
            stroke="#F28C28"
            stroke-width="3"
            stroke-linecap="round"
          />

          <!-- Courbe de Merge de 'combat' vers 'main' (Étape 4) : de (340, 48) vers (420, 94) -->
          <path
            v-if="currentStep >= 4"
            d="M 340 48 C 375 48, 390 94, 420 94"
            fill="none"
            stroke="#F28C28"
            stroke-width="3"
            stroke-linecap="round"
          />

          <!-- CERCLES DE COMMITS (Rayon 6px avec bordure blanche 2.5px) -->
          <!-- C1: Init (60, 94) -->
          <circle cx="60" cy="94" r="5.5" fill="#0E9AA7" stroke="#FFFFFF" stroke-width="2.5" />

          <!-- C2: Squelette (140, 94) -->
          <circle cx="140" cy="94" r="5.5" fill="#0E9AA7" stroke="#FFFFFF" stroke-width="2.5" />

          <!-- C3: Alice PV (220, 48) -->
          <circle v-if="currentStep >= 2" cx="220" cy="48" r="5.5" fill="#F28C28" stroke="#FFFFFF" stroke-width="2.5" />

          <!-- C4: Bob Son (270, 94) -->
          <circle v-if="currentStep >= 2" cx="270" cy="94" r="5.5" fill="#0E9AA7" stroke="#FFFFFF" stroke-width="2.5" />

          <!-- C5: Alice Attaque (330, 48) -->
          <circle v-if="currentStep >= 3" cx="330" cy="48" r="5.5" fill="#F28C28" stroke="#FFFFFF" stroke-width="2.5" />

          <!-- C6: Merge Commit (420, 94) -->
          <circle v-if="currentStep >= 4" cx="420" cy="94" r="7.5" fill="#10B981" stroke="#FFFFFF" stroke-width="3" />
        </svg>

        <!-- ZONE 3 : BADGES DE LA BRANCHE MAIN (TOUT EN BAS - Y: 114px à 136px) -->
        <div class="absolute bottom-2 left-3 right-3 z-10 flex items-center justify-between">
          <div class="flex items-center gap-1.5">
            <span class="px-2 py-0.5 rounded text-[9.5px] font-mono font-bold bg-[#0E9AA7] text-white shadow-xs inline-flex items-center gap-1">
              <lucide:git-branch class="w-2.5 h-2.5" />
              <span>main</span>
            </span>
            <span class="text-slate-400 text-[10px] inline-flex items-center gap-1">
              <lucide:user class="w-3 h-3" />
              <span>Bob</span>
            </span>
          </div>

          <!-- Pointers de commits actifs sur main (en dessous du rail, ne touche rien) -->
          <div class="flex items-center gap-1.5">
            <span
              v-if="currentStep === 1"
              class="px-1.5 py-0.2 rounded bg-[#0E9AA7]/20 border border-[#0E9AA7] text-[#0E9AA7] font-mono text-[9px] font-bold inline-flex items-center gap-1"
            >
              <span>HEAD</span>
              <lucide:arrow-right class="w-2.5 h-2.5" />
              <span>main [d4e2f]</span>
            </span>
            <span
              v-if="currentStep >= 2 && currentStep <= 3"
              class="px-1.5 py-0.2 rounded bg-[#0E9AA7]/20 border border-[#0E9AA7] text-[#0E9AA7] font-mono text-[9px] font-bold inline-flex items-center gap-1"
            >
              <lucide:headphones class="w-2.5 h-2.5" />
              <span>Son [b3f5d] · main</span>
            </span>
            <span
              v-if="currentStep >= 4"
              class="px-2 py-0.5 rounded bg-emerald-400 text-slate-950 font-mono text-[9.5px] font-black shadow-md flex items-center gap-1"
            >
              <lucide:tag class="w-3 h-3" />
              <span>v1.0 release [f8a02]</span>
            </span>
          </div>
        </div>
      </div>

      <!-- TERMINAL & LOG DU COMMIT ACTIF -->
      <div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800 text-slate-200 font-mono text-[10px] space-y-1">
        <div class="flex items-center justify-between pb-1 border-b border-slate-800 text-[9px] text-slate-400">
          <span class="text-slate-300 font-sans font-bold">{{ stepsMeta[currentStep - 1].title }}</span>
          <span class="text-[#0E9AA7]">branche active : {{ currentStep >= 2 && currentStep <= 3 ? 'combat' : 'main' }}</span>
        </div>
        <div class="flex items-center gap-1.5 text-slate-100">
          <span class="text-[#F28C28] font-bold select-none">&gt;</span>
          <span class="text-amber-300 font-semibold">{{ stepsMeta[currentStep - 1].cli }}</span>
        </div>
        <div class="text-slate-400 font-sans text-[9.5px] leading-tight">
          {{ stepsMeta[currentStep - 1].explain }}
        </div>
      </div>
    </div>
  </div>
</template>