<script setup>
defineProps({
  link: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <div class="slidev-layout title">
    <div class="flex flex-col items-center justify-center h-full">
        <h1 class="text-7xl font-bold text-center leading-tight tracking-tight pt-12">
          <slot name="title" />
        </h1>
      <h2 class="text-3xl text-center mb-4 max-w-3xl leading-relaxed">
        <slot name="subtitle" />
      </h2>
      <div class="flex flex-col items-center">
        <!-- Shadow for QR box -->
        <div class="bg-gradient-to-br from-white to-bone-white p-8 rounded-2xl shadow-2xl flex flex-col items-center">
          <div class="text-center mb-4 text-slate-steel font-medium">
            <slot name="qr-text">Scan to Follow Along</slot>
          </div>
          <div class="w-56 h-56 bg-gradient-to-br from-gray-100 to-gray-200 rounded-xl flex items-center justify-center shadow-inner">
            <img v-if="link" :src="`https://api.qrserver.com/v1/create-qr-code/?size=224x224&data=${encodeURIComponent(link)}`" alt="QR Code" class="rounded-lg" />
            <slot v-else name="qr" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>