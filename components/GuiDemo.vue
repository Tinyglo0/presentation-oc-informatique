<script setup lang="ts">
import { ref } from 'vue'

// Mini app Tkinter state
const darkApp = ref(false)
const newTask = ref('')
const tasks = ref([
  { id: 1, text: 'Créer la base SQL', done: true },
  { id: 2, text: 'Coder la fenêtre CTkinter', done: false },
])

function addTask() {
  if (!newTask.value.trim()) return
  tasks.value.push({ id: Date.now(), text: newTask.value.trim(), done: false })
  newTask.value = ''
}

// Mini game Pygame state
const score = ref(420)
const ballX = ref(50)
const ballDir = ref(1)

function bounceBall() {
  score.value += 10
  ballX.value = ballDir.value > 0 ? 82 : 18
  ballDir.value *= -1
}
</script>

<template>
  <div class="grid grid-cols-2 gap-5 items-stretch text-xs">
    <!-- Option 1: Tkinter / CTkinter -->
    <div class="p-4 rounded-2xl bg-white border-2 border-slate-200 flex flex-col justify-between shadow-xs">
      <div>
        <div class="flex items-center justify-between mb-2">
          <div class="font-extrabold text-base text-[#14213D] flex items-center gap-2">
            <span class="flex items-center gap-1.5">
              <lucide:app-window class="w-4 h-4 text-[#F28C28]" />
              <span>Option 1 : Logiciel</span>
            </span>
          </div>
          <span class="px-2 py-0.5 rounded text-[10px] font-bold bg-[#FFF4E8] text-[#F28C28] border border-orange-200">
            Tkinter / CTkinter
          </span>
        </div>
        <p class="text-[11.5px] text-slate-600 m-0 mb-2.5 leading-snug">
          Fenêtres, boutons, zones de saisie et mode sombre automatique pour concevoir une application intuitive.
        </p>

        <!-- Interactive Window Mockup -->
        <div
          class="p-3 rounded-xl border transition-colors"
          :class="darkApp ? 'bg-slate-800 border-slate-700 text-white' : 'bg-slate-50 border-slate-200 text-slate-800'"
        >
          <div class="flex items-center justify-between mb-2 pb-1.5 border-b" :class="darkApp ? 'border-slate-700' : 'border-slate-200'">
            <div class="flex items-center gap-1.5">
              <span class="w-2.5 h-2.5 rounded-full bg-red-400"></span>
              <span class="w-2.5 h-2.5 rounded-full bg-amber-400"></span>
              <span class="w-2.5 h-2.5 rounded-full bg-emerald-400"></span>
              <span class="text-[10px] font-mono ml-1 opacity-75">mon_appli.py</span>
            </div>
            <button
              @click="darkApp = !darkApp"
              class="px-2 py-0.5 rounded text-[10px] font-semibold cursor-pointer border"
              :class="darkApp ? 'bg-slate-700 border-slate-600 text-amber-300' : 'bg-white border-slate-200 text-slate-600'"
            >
              <span class="inline-flex items-center gap-1">
                <lucide:sun v-if="darkApp" class="w-3 h-3 text-amber-300" />
                <lucide:moon v-else class="w-3 h-3 text-slate-500" />
                <span>{{ darkApp ? 'Mode clair' : 'Mode sombre' }}</span>
              </span>
            </button>
          </div>

          <div class="space-y-1 mb-2 max-h-18 overflow-y-auto">
            <div
              v-for="t in tasks"
              :key="t.id"
              @click="t.done = !t.done"
              class="flex items-center gap-2 px-2 py-1 rounded cursor-pointer text-[11px]"
              :class="darkApp ? 'bg-slate-700/60' : 'bg-white'"
            >
              <input type="checkbox" v-model="t.done" class="cursor-pointer accent-[#F28C28]" />
              <span :class="{ 'line-through opacity-50': t.done }">{{ t.text }}</span>
            </div>
          </div>

          <div class="flex gap-1.5">
            <input
              v-model="newTask"
              @keyup.enter="addTask"
              placeholder="Nouvelle tâche..."
              class="flex-1 px-2 py-1 rounded text-[11px] border outline-none"
              :class="darkApp ? 'bg-slate-900 border-slate-700 text-white' : 'bg-white border-slate-200 text-slate-800'"
            />
            <button
              @click="addTask"
              class="px-2.5 py-1 rounded bg-[#F28C28] text-white font-bold text-[11px] cursor-pointer"
            >
              + Ajouter
            </button>
          </div>
        </div>
      </div>

      <div class="text-[11px] text-slate-500 mt-2.5 pt-2 border-t border-slate-100 flex items-center gap-1.5">
        <lucide:target class="w-3.5 h-3.5 text-slate-400 shrink-0" />
        <span>Idéal pour : gestionnaires, tableaux de bord, outils d'analyse.</span>
      </div>
    </div>

    <!-- Option 2: Pygame -->
    <div class="p-4 rounded-2xl bg-[#FFF4E8] border-2 border-orange-200 flex flex-col justify-between shadow-xs">
      <div>
        <div class="flex items-center justify-between mb-2">
          <div class="font-extrabold text-base text-[#14213D] flex items-center gap-2">
            <span class="flex items-center gap-1.5">
              <lucide:gamepad-2 class="w-4 h-4 text-[#F28C28]" />
              <span>Option 2 : Jeu Vidéo 2D</span>
            </span>
          </div>
          <span class="px-2 py-0.5 rounded text-[10px] font-bold bg-[#F28C28] text-white">
            Pygame
          </span>
        </div>
        <p class="text-[11.5px] text-slate-600 m-0 mb-2.5 leading-snug">
          Ajoutez images, sprites et effets sonores à 60 images/seconde pour créer votre propre jeu vidéo.
        </p>

        <!-- Interactive Pygame Mockup -->
        <div
          @click="bounceBall"
          class="p-3 rounded-xl bg-[#14213D] border border-slate-700 text-white relative h-32 flex flex-col justify-between cursor-pointer select-none overflow-hidden shadow-inner"
        >
          <div class="flex justify-between items-center text-[10px] font-mono text-slate-300">
            <span>SCORE: {{ score }}</span>
            <span class="text-[#F28C28] inline-flex items-center gap-1">
              <lucide:mouse-pointer-click class="w-3 h-3" />
              <span>Cliquez pour renvoyer la balle !</span>
            </span>
            <span class="inline-flex items-center gap-0.5">
              <span>VIES:</span>
              <lucide:heart class="w-2.5 h-2.5 text-rose-500 fill-rose-500 ml-1" />
              <lucide:heart class="w-2.5 h-2.5 text-rose-500 fill-rose-500" />
              <lucide:heart class="w-2.5 h-2.5 text-rose-500 fill-rose-500" />
            </span>
          </div>

          <div class="relative flex-1 flex items-center">
            <!-- Left Paddle -->
            <div class="w-2.5 h-12 bg-[#F28C28] rounded-sm"></div>

            <!-- Ball -->
            <div
              class="w-4 h-4 rounded-full bg-amber-400 shadow-md transition-all duration-300 absolute"
              :style="{ left: ballX + '%' }"
            ></div>

            <!-- Right Paddle -->
            <div class="w-2.5 h-12 bg-sky-400 rounded-sm ml-auto"></div>
          </div>

          <div class="text-[10px] font-mono text-center text-slate-400">
            60 FPS · Collisions · Clavier / Manette · Sons
          </div>
        </div>
      </div>

      <div class="text-[11px] text-[#F28C28] font-bold mt-2.5 pt-2 border-t border-orange-200 flex items-center gap-1.5">
        <lucide:sparkles class="w-3.5 h-3.5 text-[#F28C28] shrink-0" />
        <span>Idéal pour : plateforme, arcade, rogue-like, casse-briques, RPG 2D...</span>
      </div>
    </div>
  </div>
</template>
