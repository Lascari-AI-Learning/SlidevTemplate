---
theme: ../
layout: default
---

<script setup>
import { X, Check } from 'lucide-vue-next'
</script>

<div class="text-5xl text-center mb-8 font-bold" style="font-family: 'Styrene A', sans-serif;">Winning = a modular approach</div>

<div class="relative h-[500px] px-12">
  <!-- Continuum line with arrow -->
  <div class="absolute bottom-25 left-0 right-0">
    <div class="relative h-[3px]" style="background-color: #006b7d;">
      <!-- Arrow head -->
      <div class="absolute left-[-15px] top-1/2 transform -translate-y-1/2">
        <div class="w-0 h-0 border-r-[20px] border-y-[12px] border-y-transparent" style="border-right-color: #006b7d;"></div>
      </div>
      <div class="absolute right-[-15px] top-1/2 transform -translate-y-1/2">
        <div class="w-0 h-0 border-l-[20px] border-y-[12px] border-y-transparent" style="border-left-color: #006b7d;"></div>
      </div>
    </div>
  </div>

  <!-- Left box - Reinventing the AI wheel -->
  <v-click at="1">
    <div 
      class="absolute left-[0%] bottom-45 w-[250px] bg-white rounded-lg shadow-lg p-6 border border-gray-400"
      :class="{ 'opacity-40': $slidev.nav.clicks >= 3 }"
      style="transition: opacity 0.5s;"
    >
      <div class="flex flex-col items-center gap-3">
        <div class="w-12 h-12 rounded-full flex items-center justify-center flex-shrink-0 mb-0" style="background-color: #ff8b94; position: absolute; left: 50%; transform: translateX(-50%) translateY(-105%); z-index: 1;">
          <X class="w-6 h-6 text-white" :stroke-width="3" />
        </div>
        <div class="w-full mt-2">
          <p class="text-md font-bold mb-2 text-center mt-0">Reinventing the AI wheel</p>
          <p class="text-xs leading-relaxed text-center">Teams spend months or years developing custom models & infrastructure</p>
        </div>
      </div>
      <!-- Connecting line from left box to continuum -->
      <div class="absolute left-1/2 bottom-0 w-[2px] bg-gray-700 transform -translate-x-1/2" style="height: 60px; top: 100%;"></div>
      <!-- Add a circle at the bottom of the line to indicate the connection point -->
      <div class="absolute left-1/2" style="top: calc(100% + 60px); transform: translateX(-50%);">
        <div class="w-2 h-2 rounded-full bg-gray-700"></div>
      </div>
    </div>
  </v-click>

  <!-- Right box - Black box use of AI -->
  <v-click at="2">
    <div 
      class="absolute right-[0%] bottom-45 w-[250px] bg-white rounded-lg shadow-lg p-6 border border-gray-400"
      :class="{ 'opacity-40': $slidev.nav.clicks >= 3 }"
      style="transition: opacity 0.5s;"
    >
      <div class="flex flex-col items-center gap-3">
        <div class="w-12 h-12 rounded-full flex items-center justify-center flex-shrink-0 mb-0" style="background-color: #ff8b94; position: absolute; left: 50%; transform: translateX(-50%) translateY(-105%); z-index: 1;">
          <X class="w-6 h-6 text-white" :stroke-width="3" />
        </div>
        <div class="w-full mt-2">
          <p class="text-md font-bold mb-2 text-center mt-0">Black box use of AI</p>
          <p class="text-xs leading-relaxed text-center">Teams implement only the most basic AI features like chatbots</p>
        </div>
      </div>
      <!-- Connecting line from right box to continuum -->
       <div class="absolute left-1/2 bottom-0 w-[2px] bg-gray-700 transform -translate-x-1/2" style="height: 60px; top: 100%;"></div>
      <!-- Add a circle at the bottom of the line to indicate the connection point -->
      <div class="absolute left-1/2" style="top: calc(100% + 60px); transform: translateX(-50%);">
        <div class="w-2 h-2 rounded-full bg-gray-700"></div>
      </div>
    </div>
  </v-click>

  <!-- Middle box - LEGO block use of AI -->
  <v-click at="3">
    <div class="absolute left-1/2 bottom-45 w-[250px] transform -translate-x-1/2 bg-white rounded-lg shadow-xl p-6 border-3 z-10" style="border-color: #00d9a3;">
      <div class="flex flex-col items-center gap-3">
        <!-- The check icon is visually present but does not take up vertical space above the text -->
        <div class="w-12 h-12 rounded-full flex items-center justify-center flex-shrink-0 mb-0" style="background-color: #00d9a3; position: absolute; left: 50%; transform: translateX(-50%) translateY(-105%); z-index: 1;">
          <Check class="w-6 h-6 text-white" :stroke-width="3" />
        </div>
        <div class="w-full mt-2">
          <p class="text-md font-bold mb-2 text-center mt-0">LEGO block use of AI</p>
          <p class="text-xs leading-relaxed text-center">Teams assemble differentiated AI features by integrating the best available AI capabilities with their product's data and functionality</p>
        </div>
      </div>
      <!-- Connecting line from middle box to continuum -->
      <!-- Vertical connecting line from middle box to continuum with a circle at the bottom -->
      <div class="absolute left-1/2 bottom-0 w-[2px] bg-gray-700 transform -translate-x-1/2 mt-1" style="height: 60px; top: 100%;"></div>
      <!-- Add a circle at the bottom of the line to indicate the connection point -->
      <div class="absolute left-1/2" style="top: calc(100% + 60px); transform: translateX(-50%);">
        <div class="w-2 h-2 rounded-full bg-gray-700"></div>
      </div>
    </div>
  </v-click>
</div>

<style>
.slidev-vclick-hidden {
  opacity: 0;
}
</style>

<!--
This slide demonstrates the winning approach to AI implementation - using a modular "LEGO block" approach rather than either reinventing everything from scratch or using only basic black-box AI features.

The animation sequence:
1. First click shows the left box (Reinventing the AI wheel)
2. Second click shows the right box (Black box use of AI)
3. Third click shows the middle box (LEGO block approach) and fades the other two boxes to emphasize the winning approach
-->