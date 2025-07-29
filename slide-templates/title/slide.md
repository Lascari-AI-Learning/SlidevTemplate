---
theme: ../
layout: default
---

<script setup>
const link = '{{qr_link}}'
</script>

<div class="flex flex-col items-center justify-center h-full">
    <h1 class="text-7xl font-bold text-center leading-tight tracking-tight pt-12">
      {{title}}
    </h1>
  <h2 class="text-3xl text-center mb-4 max-w-3xl leading-relaxed">
    {{subtitle}}
  </h2>
  <div class="flex flex-col items-center">
    <!-- Shadow for QR box -->
    <div class="bg-gradient-to-br from-white to-bone-white p-8 rounded-2xl shadow-2xl flex flex-col items-center">
      <div class="text-center mb-4 text-slate-steel font-medium">
        {{qr_label}}
      </div>
      <div class="w-56 h-56 bg-gradient-to-br from-gray-100 to-gray-200 rounded-xl flex items-center justify-center shadow-inner">
        <img :src="`https://api.qrserver.com/v1/create-qr-code/?size=224x224&data=${encodeURIComponent(link)}`" alt="QR Code" class="rounded-lg" />
      </div>
    </div>
  </div>
</div>

<!--
{{speaker_notes}}
-->

<style>
  .text-slate-steel { color: #4C5A61; }
  .text-bone-white { color: #EAE7DC; }
  .text-fog-grey { color: #B0B3B8; }
  .border-iron-ochre { border-color: #A35E35; }
  .bg-obsidian-black { background-color: #0C0C0C; }
  .bg-ash-graphite { background-color: #2B2B2B; }
</style>