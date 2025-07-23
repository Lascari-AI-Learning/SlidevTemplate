---
theme: ../
---

<script setup>
// No script setup needed for this slide
</script>

<div class="slidev-layout speaker h-full flex items-center">
    <div class="grid grid-cols-5 gap-24 w-full max-w-7xl mx-auto px-6">
        <!-- Left side: Content -->
        <div class="flex flex-col col-span-3 justify-center space-y-4">
            <!-- Main content slot -->
            <div class="flex flex-col">
                <span class="text-4xl font-bold mb-2">About Me</span>
                <ul>
                    <li class="text-xl">Applied AI Engineer & Consultant</li>
                </ul>
            </div>
            <div class="flex flex-col">
                <span class="text-2xl font-semibold mt-8 mb-2">What I've Done</span>
                <ul class="space-y-3">
                    <li class="text-lg leading-relaxed">3 years Full-time in Gen AI</li>
                    <li class="text-lg leading-relaxed">Built <strong class="text-iron-ochre font-semibold">30+ Gen AI Projects</strong></li>
                </ul>
            </div>
            <div class="flex flex-col">
                <span class="text-2xl font-semibold mt-8 mb-2">Why I'm here</span>
                <ul class="space-y-3">
                    <li class="text-lg leading-relaxed">Build AI Systems that Provide <strong class="text-iron-ochre font-semibold">Real Value</strong></li>
                    <li class="text-lg leading-relaxed">Turn Years of Hard-Won Knowledge into an <strong class="text-iron-ochre font-semibold">Unfair Advantage</strong></li>
                </ul>
            </div>
        </div>
        <!-- Right side: Image with name -->
        <div class="flex flex-col items-center justify-center col-span-2">
            <!-- Name above image -->
            <span class="text-2xl font-semibold mb-6">
                Ford Lascari
            </span>
            <div class="relative">
                <!-- Image container -->
                <div class="w-[280px] h-[280px] bg-gradient-to-br from-gray-100 to-gray-200 rounded-[2.5rem] overflow-hidden shadow-2xl">
                <img src="/avatar.jpeg" class="w-full h-full object-cover" alt="Ford Lascari" />
                </div>
            </div>
        </div>
    </div>
</div>

<style scoped>
.slidev-layout.speaker {
  @apply bg-gradient-to-br from-bone-white to-gray-50;
}

/* Enhanced typography for better readability */
.slidev-layout.speaker h1 {
  font-family: 'StyreneB-Bold-Trial', system-ui, sans-serif;
  letter-spacing: -0.02em;
}

.slidev-layout.speaker h3 {
  font-family: 'StyreneB-Medium-Trial', system-ui, sans-serif;
}

.slidev-layout.speaker ul {
  @apply space-y-3;
}

.slidev-layout.speaker li {
  font-family: 'StyreneA-Regular-Trial', system-ui, sans-serif;
  @apply transition-all duration-200 ease-out;
}

.slidev-layout.speaker li:hover {
  @apply translate-x-1;
}

/* Title section styling */
.slidev-layout.speaker .text-xl {
  font-family: 'StyreneA-Regular-Trial', system-ui, sans-serif;
}

/* Color definitions */
.text-slate-steel { color: #4C5A61; }
.text-bone-white { color: #EAE7DC; }
.text-fog-grey { color: #B0B3B8; }
.text-obsidian-black { color: #0C0C0C; }
.text-ash-graphite { color: #2B2B2B; }
.text-iron-ochre { color: #A35E35; }
.bg-bone-white { background-color: #EAE7DC; }
</style>

<!--
Speaker notes:
- I've been in the trenches for 3 years - this isn't theoretical
- 30+ MVPs means I've seen EVERY way these systems fail
- 10+ in production means I know what survives contact with reality
- Your engineering instincts about testing, error handling, and architecture? They're MORE important with AI, not less
- I'm here because good engineers make the difference between toys and products
-->
