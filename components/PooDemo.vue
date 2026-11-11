<script setup lang="ts">
import { ref, computed } from 'vue'
import { ShikiMagicMovePrecompiled } from '@shikijs/magic-move/vue'
import '@shikijs/magic-move/dist/style.css'
import pooMagicSteps from './pooMagicSteps.json'

const containerRef = ref<HTMLElement>()
const globalScale = computed(() => {
  if (!containerRef.value) return 1
  const rect = containerRef.value.getBoundingClientRect()
  const offsetWidth = containerRef.value.offsetWidth
  return offsetWidth > 0 ? rect.width / offsetWidth : 1
})

const codeMode = ref<'dict' | 'oop'>('dict')
const heroPv = ref(100)
const bossPv = ref(120)
const combatLog = ref('Prêt : cliquez sur heros.attaquer(dragon) !')

function toggleCode(mode: 'dict' | 'oop') {
  codeMode.value = mode
}

function attaquerBoss() {
  if (bossPv.value <= 0) return
  if (codeMode.value === 'dict') {
    codeMode.value = 'oop'
  }
  const dmg = 25
  bossPv.value = Math.max(0, bossPv.value - dmg)
  if (bossPv.value > 0) {
    heroPv.value = Math.max(0, heroPv.value - 15)
    combatLog.value = `heros.attaquer(dragon) → Dragon -${dmg} PV · Riposte -15 PV !`
  } else {
    combatLog.value = `heros.attaquer(dragon) → Victoire ! Le Dragon est vaincu !`
  }
}

function boirePotion() {
  heroPv.value = Math.min(100, heroPv.value + 30)
  combatLog.value = `heros.soigner() → Alex récupère +30 PV !`
}

function resetCombat() {
  heroPv.value = 100
  bossPv.value = 120
  combatLog.value = 'Objets réinitialisés : heros(100 PV) & dragon(120 PV)'
}
</script>

<template>
  <div class="grid grid-cols-12 gap-3.5 items-stretch text-xs min-w-0">
    <!-- COLONNE GAUCHE : MAGIC CODE PYTHON (6 cols) -->
    <div class="col-span-6 p-2.5 rounded-xl bg-slate-50 border border-slate-200 flex flex-col justify-between space-y-2 min-w-0">
      <div class="min-w-0">
        <div class="flex items-center justify-between mb-1.5">
          <div class="flex items-center gap-2">
            <span class="w-1.5 h-1.5 rounded-full bg-[#F28C28]"></span>
            <span class="font-bold text-slate-800 text-xs">
              Structure du code
            </span>
          </div>
          <div class="flex gap-1 bg-slate-200/80 p-0.5 rounded-lg border border-slate-300 shrink-0">
            <button
              @click="toggleCode('dict')"
              class="px-2 py-0.5 rounded text-[10px] font-bold cursor-pointer transition-all"
              :class="codeMode === 'dict' ? 'bg-slate-800 text-white shadow-xs' : 'text-slate-600 hover:text-black'"
            >
              1. Dictionnaire
            </button>
            <button
              @click="toggleCode('oop')"
              class="px-2 py-0.5 rounded text-[10px] font-bold cursor-pointer transition-all"
              :class="codeMode === 'oop' ? 'bg-[#F28C28] text-white shadow-xs' : 'text-slate-600 hover:text-black'"
            >
              2. Classe (POO)
            </button>
          </div>
        </div>

        <!-- Fenêtre d'éditeur Shiki Magic Move -->
        <div ref="containerRef" class="rounded-lg bg-[#282c34] border border-slate-700 overflow-hidden shadow-xs min-w-0">
          <!-- Barre d'onglets éditeur -->
          <div class="flex items-center justify-between px-2.5 py-0.8 bg-[#21252b] text-[9.5px] font-mono border-b border-slate-700/80">
            <div class="flex items-center gap-1.5">
              <span class="w-2 h-2 rounded-full bg-red-400"></span>
              <span class="w-2 h-2 rounded-full bg-amber-400"></span>
              <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
              <span class="text-slate-300 ml-1">personnage.py</span>
            </div>
            <span class="text-[#F28C28] font-bold text-[9px]">
              {{ codeMode === 'dict' ? 'Syntaxe dictionnaire' : 'Syntaxe objet' }}
            </span>
          </div>

          <!-- Composant Shiki Magic Move fluide avec hauteur adaptée à tout le code POO -->
          <div class="p-2.5 h-[215px] overflow-hidden">
            <ShikiMagicMovePrecompiled
              :steps="pooMagicSteps"
              :step="codeMode === 'dict' ? 0 : 1"
              :animate="true"
              class="font-mono text-[9.5px] leading-relaxed select-none"
              :options="{
                duration: 750,
                delayMove: 0.25,
                delayLeave: 0,
                delayEnter: 0.65,
                stagger: 2,
                easing: 'cubic-bezier(0.25, 1, 0.5, 1)',
                globalScale: globalScale,
                animateContainer: false,
              }"
            />
          </div>
        </div>
      </div>

      <div class="p-1.5 px-2 rounded-lg bg-white border border-slate-200 text-[9.5px] text-slate-600 leading-snug flex items-center gap-1.5">
        <lucide:lightbulb class="w-3.5 h-3.5 text-amber-500 shrink-0" />
        <span>Les données <code>pv: 100</code> et <code>atk: 25</code> et la fonction <code>attaquer()</code> sont maintenant fusionnées directement dans la <strong>classe</strong> !</span>
      </div>
    </div>

    <!-- COLONNE DROITE : SIMULATEUR D'OBJETS INTERACTIFS (6 cols) -->
    <div class="col-span-6 p-2.5 rounded-xl bg-[#FFF4E8] border border-[#F28C28]/40 flex flex-col justify-between space-y-2 min-w-0">
      <div class="min-w-0">
        <div class="flex items-center justify-between mb-1.5">
          <span class="font-bold text-[#F28C28] text-[10.5px] uppercase tracking-wider truncate">
            Simulateur d'objets en direct
          </span>
          <button @click="resetCombat" class="text-[9px] underline text-slate-500 hover:text-black cursor-pointer shrink-0">
            Réinitialiser
          </button>
        </div>

        <!-- Deux cartes d'objets -->
        <div class="grid grid-cols-2 gap-2 mb-2">
          <!-- Alex -->
          <div class="p-2 rounded-xl bg-white border border-slate-200 text-center shadow-2xs min-w-0">
            <div class="h-6 flex items-center justify-center mb-1">
              <lucide:shield class="w-5 h-5 text-emerald-600" />
            </div>
            <div class="font-bold text-[#14213D] text-[10.5px] truncate">Objet <code>heros</code></div>
            <div class="text-[9px] text-slate-400 font-mono mb-1">{{ heroPv }} / 100 PV</div>
            <div class="w-full h-2 bg-slate-100 rounded-full overflow-hidden">
              <div class="h-full bg-emerald-500 transition-all duration-300" :style="{ width: heroPv + '%' }"></div>
            </div>
          </div>

          <!-- Dragon -->
          <div class="p-2 rounded-xl bg-white border border-slate-200 text-center shadow-2xs min-w-0">
            <div class="h-6 flex items-center justify-center mb-1">
              <lucide:flame v-if="bossPv > 0" class="w-5 h-5 text-[#F28C28]" />
              <lucide:skull v-else class="w-5 h-5 text-slate-400" />
            </div>
            <div class="font-bold text-[#14213D] text-[10.5px] truncate">Objet <code>dragon</code></div>
            <div class="text-[9px] text-slate-400 font-mono mb-1">{{ bossPv }} / 120 PV</div>
            <div class="w-full h-2 bg-slate-100 rounded-full overflow-hidden">
              <div class="h-full bg-[#F28C28] transition-all duration-300" :style="{ width: (bossPv / 120) * 100 + '%' }"></div>
            </div>
          </div>
        </div>

        <!-- Boutons d'appel des méthodes -->
        <div class="flex gap-2">
          <button
            @click="attaquerBoss"
            class="flex-1 py-1.5 px-2 rounded-lg bg-[#F28C28] hover:bg-orange-600 text-white font-bold text-[10px] cursor-pointer shadow-xs transition-transform active:scale-95 flex items-center justify-center gap-1.5"
          >
            <lucide:swords class="w-3.5 h-3.5" />
            <span>heros.attaquer(dragon)</span>
          </button>
          <button
            @click="boirePotion"
            class="py-1.5 px-2.5 rounded-lg bg-white border border-[#F28C28] text-[#F28C28] font-bold text-[10px] cursor-pointer hover:bg-orange-50 transition-transform active:scale-95 flex items-center gap-1.5"
          >
            <lucide:flask-conical class="w-3.5 h-3.5" />
            <span>soigner()</span>
          </button>
        </div>
      </div>

      <!-- Journal console de l'interaction -->
      <div class="p-2 rounded-lg bg-[#14213D] text-slate-200 font-mono text-[9px] border border-slate-700/80 leading-tight truncate">
        <span class="text-[#0E9AA7] font-bold select-none">&gt;</span> {{ combatLog }}
      </div>
    </div>
  </div>
</template>

<style>
/* Fenêtre de code stable et transitions Magic Move fluides */
.shiki-magic-move-container {
  white-space: pre !important;
}
.shiki-magic-move-container-resize {
  transition: none !important;
}
.shiki-magic-move-move,
.shiki-magic-move-enter-active,
.shiki-magic-move-leave-active {
  will-change: transform, opacity;
}
.shiki-magic-move-enter-from,
.shiki-magic-move-leave-to {
  opacity: 0;
}
</style>