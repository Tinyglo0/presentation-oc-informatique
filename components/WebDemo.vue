<script setup lang="ts">
import { ref } from 'vue'

const mode = ref<'raw' | 'modern' | 'cyber'>('modern')
const likes = ref(42)

const cssSnippets = {
  raw: '/* Aucun style CSS appliqué */\n/* Affichage standard du navigateur */',
  modern: '.carte {\n  background: white;\n  border-radius: 12px;\n  box-shadow: 0 8px 20px #0001;\n}',
  cyber: '.carte {\n  background: #14213D;\n  border: 2px solid #F28C28;\n  color: white;\n}',
}
</script>

<template>
  <div class="grid grid-cols-12 gap-3.5 items-stretch text-xs">
    <!-- COLONNE GAUCHE : CODE HTML & CSS (6 cols) -->
    <div class="col-span-6 flex flex-col justify-between space-y-2 min-w-0">
      <!-- Les 2 piliers en 1 ligne compacte -->
      <div class="grid grid-cols-2 gap-2">
        <div class="p-2 rounded-lg bg-orange-50 border border-orange-200 flex items-center gap-2">
          <lucide:boxes class="w-4 h-4 text-orange-600 shrink-0" />
          <div class="min-w-0">
            <div class="font-bold text-orange-800 text-[11px] truncate">HTML5 (Structure)</div>
            <div class="text-[9.5px] text-slate-600 truncate">Titres, boutons, blocs</div>
          </div>
        </div>
        <div class="p-2 rounded-lg bg-sky-50 border border-sky-200 flex items-center gap-2">
          <lucide:palette class="w-4 h-4 text-sky-600 shrink-0" />
          <div class="min-w-0">
            <div class="font-bold text-sky-800 text-[11px] truncate">CSS3 (Style)</div>
            <div class="text-[9.5px] text-slate-600 truncate">Couleurs, design, layout</div>
          </div>
        </div>
      </div>

      <!-- Sélecteur de style interactif -->
      <div class="p-2.5 rounded-xl bg-slate-50 border border-slate-200 flex flex-col justify-between space-y-2 min-w-0">
        <div class="flex items-center justify-between">
          <span class="font-bold text-slate-700 text-[10.5px] uppercase tracking-wider">
            Effet du CSS en direct :
          </span>
          <div class="flex gap-1">
            <button
              @click="mode = 'raw'"
              class="px-2 py-0.5 rounded text-[10px] font-bold cursor-pointer transition-all border"
              :class="mode === 'raw' ? 'bg-slate-800 text-white border-slate-800 shadow-xs' : 'bg-white text-slate-600 border-slate-200 hover:border-slate-400'"
            >
              1. HTML seul
            </button>
            <button
              @click="mode = 'modern'"
              class="px-2 py-0.5 rounded text-[10px] font-bold cursor-pointer transition-all border"
              :class="mode === 'modern' ? 'bg-[#0E9AA7] text-white border-[#0E9AA7] shadow-xs' : 'bg-white text-slate-600 border-slate-200 hover:border-[#0E9AA7]'"
            >
              2. Moderne
            </button>
            <button
              @click="mode = 'cyber'"
              class="px-2 py-0.5 rounded text-[10px] font-bold cursor-pointer transition-all border"
              :class="mode === 'cyber' ? 'bg-[#F28C28] text-white border-[#F28C28] shadow-xs' : 'bg-white text-slate-600 border-slate-200 hover:border-[#F28C28]'"
            >
              3. Gaming
            </button>
          </div>
        </div>

        <!-- Éditeur de code HTML (fixe) -->
        <div class="rounded-lg bg-[#14213D] border border-slate-700 overflow-hidden shadow-xs min-w-0">
          <div class="flex items-center justify-between px-2.5 py-0.8 bg-slate-800/90 text-[9.5px] font-mono border-b border-slate-700">
            <span class="text-slate-300 inline-flex items-center gap-1"><lucide:file-code class="w-3 h-3 text-sky-400" /> index.html</span>
            <span class="text-[#0E9AA7] font-semibold text-[9px]">Le HTML ne change pas</span>
          </div>
          <pre class="p-2 text-[10px] leading-tight font-mono text-sky-200 m-0 overflow-x-auto whitespace-pre max-w-full"><code>&lt;div class="carte"&gt;
  &lt;h3&gt;Alex · Niv. 42&lt;/h3&gt;
  &lt;p&gt;Projet OC Info&lt;/p&gt;
  &lt;button&gt;Soutenir&lt;/button&gt;
&lt;/div&gt;</code></pre>
        </div>

        <!-- Éditeur CSS dynamique -->
        <div class="rounded-lg bg-[#1e293b] border border-slate-700 overflow-hidden shadow-xs min-w-0">
          <div class="flex items-center justify-between px-2.5 py-0.8 bg-slate-800 text-[9.5px] font-mono border-b border-slate-700">
            <span class="text-slate-300 inline-flex items-center gap-1"><lucide:palette class="w-3 h-3 text-amber-400" /> style.css</span>
            <span class="text-[#F28C28] font-semibold text-[9px]">
              {{ mode === 'raw' ? 'Désactivé' : mode === 'modern' ? 'Thème clair' : 'Thème dark' }}
            </span>
          </div>
          <pre class="p-2 text-[10px] leading-tight font-mono text-amber-200 m-0 overflow-x-auto whitespace-pre max-w-full"><code>{{ cssSnippets[mode] }}</code></pre>
        </div>
      </div>
    </div>

    <!-- COLONNE DROITE : APERÇU DU NAVIGATEUR (6 cols) -->
    <div class="col-span-6 flex flex-col justify-between min-w-0">
      <div class="rounded-2xl border border-slate-200 overflow-hidden shadow-md flex-1 flex flex-col bg-white min-w-0">
        <!-- Barre de navigation web miniature -->
        <div class="flex items-center gap-2 px-3 py-1.5 bg-slate-100 border-b border-slate-200 text-[10px] text-slate-500">
          <div class="flex items-center gap-1">
            <span class="w-2 h-2 rounded-full bg-red-400"></span>
            <span class="w-2 h-2 rounded-full bg-amber-400"></span>
            <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
          </div>
          <div class="flex-1 bg-white px-2 py-0.5 rounded border border-slate-200 font-mono text-[9px] text-slate-600 truncate">
            https://oc-info.ch/projet-alex
          </div>
        </div>

        <!-- Zone de rendu web dynamique -->
        <!-- 1. HTML BRUT -->
        <div
          v-if="mode === 'raw'"
          class="p-4 flex-1 flex flex-col justify-center font-serif text-black bg-white"
        >
          <div class="text-[9.5px] font-sans text-slate-400 uppercase mb-2">Rendu brut du navigateur (sans CSS) :</div>
          <h3 class="text-base font-bold m-0 mb-1">Alex · Niv. 42</h3>
          <p class="text-xs m-0 mb-3">Projet OC Info</p>
          <div>
            <button @click="likes++" class="inline-flex items-center gap-1.5 border border-gray-600 bg-gray-100 px-2.5 py-1 text-xs cursor-pointer active:bg-gray-200">
              <lucide:heart class="w-3 h-3 text-red-500 fill-red-500" />
              <span>Soutenir ({{ likes }})</span>
            </button>
          </div>
        </div>

        <!-- 2. CSS MODERNE -->
        <div
          v-else-if="mode === 'modern'"
          class="p-4 flex-1 flex flex-col justify-center items-center bg-gradient-to-b from-[#EEF6F8]/60 to-white text-center"
        >
          <div class="w-full max-w-[240px] p-3.5 rounded-xl bg-white border border-slate-200 shadow-md">
            <div class="w-10 h-10 rounded-full bg-[#0E9AA7]/15 text-[#0E9AA7] flex items-center justify-center mx-auto mb-1">
              <lucide:gamepad-2 class="w-5 h-5 text-[#0E9AA7]" />
            </div>
            <div class="font-extrabold text-sm text-[#14213D]">
              Alex <span class="px-1.5 py-0.2 rounded-full text-[9px] font-bold bg-[#0E9AA7] text-white">Niv. 42</span>
            </div>
            <div class="text-[10.5px] text-slate-500 mb-2">Projet OC Info</div>
            <button
              @click="likes++"
              class="w-full py-1.5 rounded-lg bg-[#0E9AA7] hover:bg-[#0c8591] text-white text-xs font-bold cursor-pointer shadow-xs transition-transform active:scale-95 flex items-center justify-center gap-1.5"
            >
              <lucide:heart class="w-3.5 h-3.5 fill-white" />
              <span>Soutenir ({{ likes }})</span>
            </button>
          </div>
          <div class="text-[9px] text-slate-400 mt-2">Cliquez pour tester l'interactivité !</div>
        </div>

        <!-- 3. CSS GAMING DARK -->
        <div
          v-else
          class="p-4 flex-1 flex flex-col justify-center items-center bg-[#0d1527] text-center"
        >
          <div class="w-full max-w-[240px] p-3.5 rounded-xl bg-[#14213D] border-2 border-[#F28C28] shadow-lg text-white">
            <div class="w-10 h-10 rounded-xl bg-[#F28C28]/20 border border-[#F28C28] text-[#F28C28] flex items-center justify-center mx-auto mb-1">
              <lucide:gamepad class="w-5 h-5 text-[#F28C28]" />
            </div>
            <div class="font-black text-sm text-white">
              Alex <span class="px-1.5 py-0.2 rounded text-[9px] font-mono font-bold bg-[#F28C28] text-[#14213D]">LVL 42</span>
            </div>
            <div class="text-[10.5px] text-slate-300 mb-2">Projet OC Info</div>
            <button
              @click="likes++"
              class="w-full py-1.5 rounded-full bg-gradient-to-r from-[#F28C28] to-amber-500 text-[#14213D] text-xs font-black cursor-pointer shadow-xs transition-transform active:scale-95 flex items-center justify-center gap-1.5"
            >
              <lucide:zap class="w-3.5 h-3.5 fill-current" />
              <span>BOOST ({{ likes }})</span>
            </button>
          </div>
          <div class="text-[9px] text-slate-400 font-mono mt-2">Même HTML · Nouveau design !</div>
        </div>
      </div>
    </div>
  </div>
</template>