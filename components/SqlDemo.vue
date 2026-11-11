<script setup lang="ts">
import { ref, computed } from 'vue'

const activeFilter = ref<'all' | 'rpg' | 'top'>('all')

const games = [
  { id: 1, titre: 'Zelda: BotW', genre: 'Aventure', note: 9.7, ventes: '31.5 M' },
  { id: 2, titre: 'Baldur’s Gate 3', genre: 'RPG', note: 9.8, ventes: '15.0 M' },
  { id: 3, titre: 'Elden Ring', genre: 'RPG', note: 9.6, ventes: '25.0 M' },
  { id: 4, titre: 'Hollow Knight', genre: 'Metroidvania', note: 9.4, ventes: '6.0 M' },
  { id: 5, titre: 'Minecraft', genre: 'Survie', note: 9.5, ventes: '300.0 M' },
  { id: 6, titre: 'Super Mario Odyssey', genre: 'Plateforme', note: 9.7, ventes: '28.0 M' },
  { id: 7, titre: 'The Witcher 3', genre: 'RPG', note: 9.5, ventes: '50.0 M' },
  { id: 8, titre: 'Celeste', genre: 'Plateforme', note: 9.3, ventes: '2.2 M' },
  { id: 9, titre: 'Cyberpunk 2077', genre: 'RPG', note: 8.8, ventes: '25.0 M' },
  { id: 10, titre: 'Hades', genre: 'Roguelike', note: 9.3, ventes: '6.5 M' },
]

const sqlQuery = computed(() => {
  if (activeFilter.value === 'rpg') {
    return `SELECT titre, genre, note, ventes\nFROM jeux\nWHERE genre = 'RPG';`
  }
  if (activeFilter.value === 'top') {
    return `SELECT titre, genre, note, ventes\nFROM jeux\nWHERE note >= 9.5\nORDER BY note DESC;`
  }
  return `SELECT titre, genre, note, ventes\nFROM jeux;`
})

const filteredGames = computed(() => {
  if (activeFilter.value === 'rpg') {
    return games.filter(g => g.genre === 'RPG')
  }
  if (activeFilter.value === 'top') {
    return [...games].filter(g => g.note >= 9.5).sort((a, b) => b.note - a.note)
  }
  return games
})
</script>

<template>
  <div class="grid grid-cols-12 gap-3.5 items-stretch text-xs">
    <!-- Colonne gauche : Requêtes SQL & Éditeur -->
    <div class="col-span-5 flex flex-col justify-between p-3.5 rounded-xl bg-slate-50 border border-slate-200">
      <div>
        <div class="font-bold text-slate-600 uppercase text-[11px] mb-1.5 flex items-center justify-between">
          <span>1. Choisissez une requête SQL</span>
          <span class="text-[10px] font-normal text-slate-400">Cliquez pour tester</span>
        </div>
        <div class="flex flex-wrap gap-1.5 mb-2.5">
          <button
            @click="activeFilter = 'all'"
            class="px-2.5 py-1 rounded-md font-semibold transition-all cursor-pointer border text-[11px]"
            :class="activeFilter === 'all' ? 'bg-[#0E9AA7] text-white border-[#0E9AA7]' : 'bg-white text-slate-600 border-slate-200 hover:border-[#0E9AA7]'"
          >
            Tout voir
          </button>
          <button
            @click="activeFilter = 'rpg'"
            class="px-2.5 py-1 rounded-md font-semibold transition-all cursor-pointer border text-[11px]"
            :class="activeFilter === 'rpg' ? 'bg-[#0E9AA7] text-white border-[#0E9AA7]' : 'bg-white text-slate-600 border-slate-200 hover:border-[#0E9AA7]'"
          >
            Filtrer : RPG
          </button>
          <button
            @click="activeFilter = 'top'"
            class="px-2.5 py-1 rounded-md font-semibold transition-all cursor-pointer border text-[11px]"
            :class="activeFilter === 'top' ? 'bg-[#0E9AA7] text-white border-[#0E9AA7]' : 'bg-white text-slate-600 border-slate-200 hover:border-[#0E9AA7]'"
          >
            Top Notes ≥ 9.5
          </button>
        </div>

        <!-- Terminal SQL -->
        <div class="rounded-lg bg-[#14213D] border border-slate-700/80 overflow-hidden shadow-inner">
          <div class="flex items-center justify-between px-2.5 py-1 bg-slate-800/90 text-[10px] font-mono border-b border-slate-700 text-slate-400">
            <span class="inline-flex items-center gap-1.5 text-slate-300">
              <lucide:terminal class="w-3.5 h-3.5 text-[#0E9AA7]" />
              requete.sql
            </span>
            <span class="text-[9.5px] text-emerald-400 font-sans font-semibold">Exécution instantanée</span>
          </div>
          <div class="p-3 text-emerald-300 font-mono text-[11.5px] leading-relaxed whitespace-pre h-[106px] flex items-center">{{ sqlQuery }}</div>
        </div>

        <!-- Schéma rapide de la base -->
        <div class="mt-2.5 p-2 rounded-lg bg-white border border-slate-200/80 text-[10.5px] text-slate-500 space-y-0.5">
          <div class="font-bold text-slate-700 flex items-center gap-1.5">
            <lucide:database class="w-3.5 h-3.5 text-[#0E9AA7]" />
            <span>Table <code>jeux</code> (4 colonnes, 10 enregistrements)</span>
          </div>
          <div class="font-mono text-[9.5px] text-slate-400">
            titre (TEXT) · genre (TEXT) · note (FLOAT) · ventes (TEXT)
          </div>
        </div>
      </div>

      <div class="mt-2.5 pt-2 border-t border-slate-200 text-[11px] text-slate-500 flex items-center gap-1.5">
        <lucide:file-text class="w-3.5 h-3.5 text-slate-400 shrink-0" />
        <span>Source : fichier brut <code>jeux.csv</code> (interrogé en &lt; 1 ms)</span>
      </div>
    </div>

    <!-- Colonne droite : Résultat SQL & Tableau dynamique -->
    <div class="col-span-7 p-3.5 rounded-xl bg-[#EEF6F8] border border-[#0E9AA7]/30 flex flex-col justify-between">
      <div>
        <div class="flex items-center justify-between mb-2">
          <span class="font-bold text-[#0E9AA7] uppercase text-[11px]">
            2. Résultat de la base de données ({{ filteredGames.length }} lignes)
          </span>
          <span class="px-2 py-0.5 rounded-full bg-white text-[#0E9AA7] font-mono text-[10px] font-bold">
            SQL Actif
          </span>
        </div>

        <!-- Conteneur de tableau à hauteur 100% stable -->
        <div class="bg-white rounded-lg border border-[#0E9AA7]/20 shadow-xs flex flex-col justify-between h-[278px] overflow-hidden">
          <table class="w-full text-left border-collapse sql-table">
            <thead>
              <tr class="bg-slate-100 text-slate-500 font-mono text-[10px] border-b border-slate-200">
                <th>titre</th>
                <th>genre</th>
                <th>note</th>
                <th>ventes</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="g in filteredGames"
                :key="g.id"
                class="border-b border-slate-100 last:border-none hover:bg-[#EEF6F8]/50 transition-colors"
              >
                <td class="font-bold text-[#14213D] text-xs">{{ g.titre }}</td>
                <td>
                  <span
                    class="px-2 py-0.5 rounded text-[10px] font-semibold"
                    :class="g.genre === 'RPG' ? 'bg-[#0E9AA7]/15 text-[#0E9AA7]' : 'bg-slate-100 text-slate-600'"
                  >
                    {{ g.genre }}
                  </span>
                </td>
                <td class="font-mono font-bold text-amber-600 text-xs">
                  <span class="inline-flex items-center gap-1">
                    <lucide:star class="w-3.5 h-3.5 fill-amber-400 text-amber-500" />
                    {{ g.note }}
                  </span>
                </td>
                <td class="text-slate-500 font-mono text-[10.5px]">{{ g.ventes }}</td>
              </tr>
            </tbody>
          </table>

          <!-- Panneau d'explication pédagogique intégré dans le tableau pour stabiliser l'espace -->
          <div
            v-if="activeFilter !== 'all'"
            class="p-3 bg-slate-50 border-t border-slate-200/80 flex-1 flex flex-col justify-center space-y-1.5"
          >
            <div class="flex items-center justify-between font-bold text-[11px] text-[#0E9AA7]">
              <span class="inline-flex items-center gap-1.5">
                <lucide:filter class="w-4 h-4 text-[#0E9AA7]" />
                <span>Clause : <code class="text-slate-800">{{ activeFilter === 'rpg' ? "WHERE genre = 'RPG'" : "WHERE note >= 9.5 ORDER BY note DESC" }}</code></span>
              </span>
              <span class="font-mono text-[10px] text-slate-500 font-bold">{{ filteredGames.length }} résultats / 10 jeux</span>
            </div>
            <p class="text-[10.5px] text-slate-600 m-0 leading-relaxed">
              {{ activeFilter === 'rpg'
                ? "Seuls les 4 RPG sont extraits. Les 6 autres jeux (Aventure, Metroidvania, Survie, Plateforme, Roguelike) sont automatiquement écartés du jeu de données."
                : "Seuls les 6 jeux avec une note ≥ 9.5 sont conservés, automatiquement triés du score le plus élevé au plus bas."
              }}
            </p>
          </div>
        </div>
      </div>

      <div class="text-[11px] text-slate-600 mt-2.5 flex items-center gap-1.5">
        <lucide:lightbulb class="w-3.5 h-3.5 text-amber-500 shrink-0" />
        <span>Sur Spotify, Netflix ou Instagram, chaque recherche exécute ce type de requête sur des millions de lignes.</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.sql-table :deep(th),
.sql-table :deep(td),
.sql-table th,
.sql-table td {
  padding-top: 4px !important;
  padding-bottom: 4px !important;
  padding-left: 10px !important;
  padding-right: 10px !important;
  line-height: 1.35 !important;
}
</style>
