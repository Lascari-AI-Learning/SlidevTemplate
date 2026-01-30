<script setup lang="ts">
import { computed, ref, onMounted, watch, nextTick } from 'vue'
import { codeToHtml } from 'shiki'

interface TerminalLine {
  command: string
  output?: string
  prompt?: string
}

const props = withDefaults(defineProps<{
  lines?: TerminalLine[]
  command?: string
  output?: string
  prompt?: string
  shell?: 'bash' | 'zsh' | 'powershell' | 'cmd'
  title?: string
  height?: number
  copyable?: boolean
  animated?: boolean
}>(), {
  prompt: '$',
  shell: 'bash',
  copyable: true,
  animated: false
})

const highlightedCommands = ref<Map<number, string>>(new Map())
const highlightedOutputs = ref<Map<number, string>>(new Map())
const isHighlighting = ref(false)
const copiedIndex = ref<number | null>(null)

// Animation state
const visibleLines = ref(0)
const currentCharIndex = ref(0)
const isTyping = ref(false)
const showOutputMap = ref<Map<number, boolean>>(new Map())
const typingInterval = ref<ReturnType<typeof setInterval> | null>(null)

const startTyping = (lineIndex: number) => {
  const line = terminalLines.value[lineIndex]
  if (!line) return

  currentCharIndex.value = 0
  isTyping.value = true

  typingInterval.value = setInterval(() => {
    currentCharIndex.value++
    if (currentCharIndex.value >= line.command.length) {
      if (typingInterval.value) clearInterval(typingInterval.value)
      typingInterval.value = null
      onTypingComplete(lineIndex)
    }
  }, 50)
}

const onTypingComplete = (lineIndex: number) => {
  isTyping.value = false
  // Brief pause before showing output
  setTimeout(() => {
    showOutputMap.value.set(lineIndex, true)
  }, 300)
}

const activateNextLine = () => {
  if (!props.animated) return
  const nextIndex = visibleLines.value
  if (nextIndex >= terminalLines.value.length) return
  visibleLines.value = nextIndex + 1
  nextTick(() => {
    startTyping(nextIndex)
  })
}

// Note: animation auto-start is handled in the merged onMounted below

defineExpose({ activateNextLine })

const terminalLines = computed(() => {
  if (props.lines && props.lines.length > 0) {
    return props.lines.map((line, idx) => ({
      command: line.command,
      output: line.output,
      prompt: line.prompt || props.prompt,
      index: idx
    }))
  }

  if (props.command) {
    return [{
      command: props.command,
      output: props.output,
      prompt: props.prompt,
      index: 0
    }]
  }

  return []
})

const getPromptColor = (shell: string) => {
  // Use subtle colors that match the overall design
  const colors = {
    bash: 'text-gray-400',
    zsh: 'text-gray-400',
    powershell: 'text-gray-400',
    cmd: 'text-gray-400'
  }
  return colors[shell] || colors.bash
}

const highlightCommand = async (command: string, index: number) => {
  if (!command.trim()) {
    highlightedCommands.value.set(index, '')
    return
  }

  try {
    isHighlighting.value = true
    const html = await codeToHtml(command, {
      lang: props.shell === 'powershell' ? 'powershell' : 'bash',
      theme: 'github-dark'
    })
    highlightedCommands.value.set(index, html)
  } catch (error) {
    console.error('Failed to highlight command:', error)
    highlightedCommands.value.set(index, '')
  } finally {
    isHighlighting.value = false
  }
}

const highlightOutput = async (output: string, index: number) => {
  if (!output || !output.trim()) {
    highlightedOutputs.value.set(index, '')
    return
  }

  // Try to detect output type - if it looks like JSON, highlight as JSON
  // Otherwise, treat as plain text
  let lang = 'text'
  const trimmed = output.trim()
  if ((trimmed.startsWith('{') && trimmed.endsWith('}')) ||
      (trimmed.startsWith('[') && trimmed.endsWith(']'))) {
    lang = 'json'
  } else if (trimmed.includes('error') || trimmed.includes('Error')) {
    lang = 'text'
  }

  try {
    const html = await codeToHtml(output, {
      lang,
      theme: 'github-dark'
    })
    highlightedOutputs.value.set(index, html)
  } catch (error) {
    // If highlighting fails, just store as plain text
    highlightedOutputs.value.set(index, '')
  }
}

const copyToClipboard = async (text: string, index: number) => {
  try {
    await navigator.clipboard.writeText(text)
    copiedIndex.value = index
    setTimeout(() => {
      copiedIndex.value = null
    }, 2000)
  } catch (error) {
    console.error('Failed to copy:', error)
  }
}

onMounted(() => {
  // Highlight all commands and outputs
  terminalLines.value.forEach((line, idx) => {
    highlightCommand(line.command, idx)
    if (line.output) {
      highlightOutput(line.output, idx)
    }
  })

  // Auto-start first line animation when animated mode is enabled
  if (props.animated && terminalLines.value.length > 0) {
    activateNextLine()
  }
})

watch(() => props.lines, () => {
  highlightedCommands.value.clear()
  highlightedOutputs.value.clear()
  terminalLines.value.forEach((line, idx) => {
    highlightCommand(line.command, idx)
    if (line.output) {
      highlightOutput(line.output, idx)
    }
  })
}, { deep: true })

watch(() => props.command, () => {
  highlightedCommands.value.clear()
  highlightedOutputs.value.clear()
  terminalLines.value.forEach((line, idx) => {
    highlightCommand(line.command, idx)
    if (line.output) {
      highlightOutput(line.output, idx)
    }
  })
})
</script>

<template>
  <div
    class="rounded-lg overflow-hidden shadow-sm border border-gray-200 dark:border-gray-700 bg-white dark:bg-[#1e1e1e] text-left"
    :style="{ height: height ? `${height}px` : 'auto' }"
  >
    <!-- Terminal Header - macOS Window Chrome -->
    <div class="flex items-center px-4 py-2 border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-[#252526] relative">
      <!-- Traffic Light Dots -->
      <div class="flex items-center gap-2">
        <div class="w-3 h-3 rounded-full" style="background-color: #FF5F56;"></div>
        <div class="w-3 h-3 rounded-full" style="background-color: #FFBD2E;"></div>
        <div class="w-3 h-3 rounded-full" style="background-color: #27C93F;"></div>
      </div>
      <!-- Centered Title -->
      <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
        <span class="text-xs font-medium text-gray-500 dark:text-gray-400">
          {{ title || shell }}
        </span>
      </div>
    </div>

    <!-- Terminal Content -->
    <div class="p-4 font-mono text-sm bg-[#0d1117]" :style="{ height: height ? `calc(${height}px - 41px)` : 'auto', overflow: height ? 'auto' : 'visible' }">
      <!-- Static Mode (animated=false) -->
      <template v-if="!animated">
        <div v-for="(line, idx) in terminalLines" :key="idx" class="mb-4 last:mb-0">
          <!-- Command Line -->
          <div class="flex items-start gap-2 mb-1">
            <span :class="['flex-shrink-0', getPromptColor(shell)]">{{ line.prompt }}</span>
            <div class="flex-1 min-w-0">
              <div class="flex items-start gap-2 group">
                <div
                  v-if="highlightedCommands.get(idx) && !isHighlighting"
                  class="flex-1 shiki-wrapper"
                  v-html="highlightedCommands.get(idx)"
                ></div>
                <pre
                  v-else
                  class="flex-1 text-gray-300 whitespace-pre-wrap break-words"
                >{{ line.command }}</pre>
                <button
                  v-if="copyable"
                  @click="copyToClipboard(line.command, idx)"
                  class="opacity-0 group-hover:opacity-100 transition-opacity flex-shrink-0 p-1 hover:bg-gray-800 rounded text-gray-500 hover:text-gray-300"
                  :title="copiedIndex === idx ? 'Copied!' : 'Copy command'"
                >
                  <span v-if="copiedIndex === idx" class="i-carbon:checkmark text-xs"></span>
                  <span v-else class="i-carbon:copy text-xs"></span>
                </button>
              </div>
            </div>
          </div>

          <!-- Output -->
          <div v-if="line.output" class="ml-6 mt-1 text-gray-400">
            <div
              v-if="highlightedOutputs.get(idx)"
              class="shiki-wrapper"
              v-html="highlightedOutputs.get(idx)"
            ></div>
            <pre
              v-else
              class="whitespace-pre-wrap break-words"
            >{{ line.output }}</pre>
          </div>
        </div>
      </template>

      <!-- Animated Mode (animated=true) -->
      <template v-else>
        <div v-for="(line, idx) in terminalLines" :key="idx" class="mb-4 last:mb-0">
          <template v-if="idx < visibleLines">
            <!-- Command Line (animated) -->
            <div class="flex items-start gap-2 mb-1">
              <span :class="['flex-shrink-0', getPromptColor(shell)]">{{ line.prompt }}</span>
              <div class="flex-1 min-w-0">
                <div class="flex items-start gap-2">
                  <!-- Currently typing line: show partial text + cursor -->
                  <template v-if="idx === visibleLines - 1 && isTyping">
                    <pre class="flex-1 text-gray-300 whitespace-pre-wrap break-words">{{ line.command.substring(0, currentCharIndex) }}<span class="terminal-cursor"></span></pre>
                  </template>
                  <!-- Finished typing: show full highlighted command -->
                  <template v-else>
                    <div
                      v-if="highlightedCommands.get(idx) && !isHighlighting"
                      class="flex-1 shiki-wrapper"
                      v-html="highlightedCommands.get(idx)"
                    ></div>
                    <pre
                      v-else
                      class="flex-1 text-gray-300 whitespace-pre-wrap break-words"
                    >{{ line.command }}</pre>
                  </template>
                </div>
              </div>
            </div>

            <!-- Output (animated: only shown after typing completes) -->
            <div v-if="line.output && showOutputMap.get(idx)" class="ml-6 mt-1 text-gray-400">
              <div
                v-if="highlightedOutputs.get(idx)"
                class="shiki-wrapper"
                v-html="highlightedOutputs.get(idx)"
              ></div>
              <pre
                v-else
                class="whitespace-pre-wrap break-words"
              >{{ line.output }}</pre>
            </div>
          </template>
        </div>
      </template>
    </div>
  </div>
</template>

<style scoped>
.shiki-wrapper {
  margin: 0;
}

.shiki-wrapper :deep(pre) {
  margin: 0;
  padding: 0;
  background: transparent !important;
}

.shiki-wrapper :deep(code) {
  font-family: 'Fira Code', 'Consolas', 'Monaco', monospace;
  font-size: 0.875rem;
  line-height: 1.5;
  display: block;
  width: 100%;
}

/* Blinking cursor for animated typing mode */
@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

.terminal-cursor {
  display: inline-block;
  width: 2px;
  height: 1em;
  background: #e5e7eb;
  vertical-align: text-bottom;
  animation: blink 1s step-end infinite;
  margin-left: 1px;
}
</style>
