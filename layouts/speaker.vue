<template>
  <div class="slidev-layout speaker h-full flex items-center">
    <div class="grid grid-cols-3 gap-12 w-full max-w-7xl mx-auto px-12">
      <!-- Left side: Content -->
      <div class="flex flex-col col-span-2 justify-center space-y-4">
        <slot />
      </div>
      
      <!-- Right side: Image with name -->
      <div class="flex flex-col items-center justify-center col-span-1">
        <!-- Name above image -->
        <h2 class="text-2xl font-semibold text-obsidian-black mb-6">
          <slot name="speaker-name">Speaker Name</slot>
        </h2>
        <div class="relative">
          <!-- Image container -->
          <div class="w-[280px] h-[280px] bg-gradient-to-br from-gray-100 to-gray-200 rounded-[2.5rem] overflow-hidden shadow-2xl">
            <slot name="image">
              <!-- Default placeholder if no image is provided -->
              <div class="w-full h-full flex items-center justify-center text-gray-400">
                <span class="text-xl">Speaker Image</span>
              </div>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.slidev-layout.speaker {
  @apply bg-gradient-to-br from-bone-white to-gray-50;
}

/* Enhanced typography for better readability */
.slidev-layout.speaker :deep(h1) {
  @apply text-4xl font-bold text-obsidian-black mb-2;
  font-family: 'StyreneB-Bold-Trial', system-ui, sans-serif;
  letter-spacing: -0.02em;
}

.slidev-layout.speaker :deep(h3) {
  @apply text-2xl font-semibold text-slate-steel mt-8;
  font-family: 'StyreneB-Medium-Trial', system-ui, sans-serif;
}

.slidev-layout.speaker :deep(ul) {
  @apply space-y-3;
}

.slidev-layout.speaker :deep(li) {
  @apply text-lg leading-relaxed text-ash-graphite;
  font-family: 'StyreneA-Regular-Trial', system-ui, sans-serif;
}

.slidev-layout.speaker :deep(strong) {
  @apply text-iron-ochre font-semibold;
}

/* Subtle animation on hover */
.slidev-layout.speaker :deep(li) {
  @apply transition-all duration-200 ease-out;
}

.slidev-layout.speaker :deep(li:hover) {
  @apply translate-x-1;
}

/* Title section styling */
.slidev-layout.speaker :deep(.text-xl) {
  @apply text-2xl text-fog-grey;
  font-family: 'StyreneA-Regular-Trial', system-ui, sans-serif;
}
</style>
