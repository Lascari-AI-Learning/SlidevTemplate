---
theme: ../
layout: default
---
<div class="text-4xl text-center mb-4">Claude Code: The Agentic Primitive</div>

<div class="rounded-xl p-4 shadow-xl text-xs border-1 border-gray-400" style="background-color: #E3DACC;">  
  <!--
    Changed p-6 to p-4 and added text-xs to make all text smaller.
    Also, removed text-sm from the inner grid to ensure all text is extra small.
    This makes the entire tools box and its contents smaller and more compact.
  -->
  <div class="grid grid-cols-2 gap-3">
    <!-- Left Column Tools -->
    <div class="space-y-6">
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500" :class="{ 'animate-pulse-border': $clicks >= 1 }">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">Agent</span>
        <span >Runs a sub-agent to handle complex, multi-step tasks</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">Bash</span>
        <span >Executes shell commands in your environment</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">Edit</span>
        <span >Makes targeted edits to specific files</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">Glob</span>
        <span >Finds files based on pattern matching</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">Grep</span>
        <span >Searches for patterns in file contents</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">LS</span>
        <span >Lists files and directories</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">MultiEdit</span>
        <span >Performs multiple edits on a single file atomically</span>
      </div>
    </div>
    <!-- Right Column Tools -->
    <div class="space-y-6">
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">NotebookEdit</span>
        <span >Modifies Jupyter notebook cells</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">NotebookRead</span>
        <span >Reads and displays Jupyter notebook contents</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">Read</span>
        <span >Reads the contents of files</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">TodoRead</span>
        <span >Reads the current session's task list</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">TodoWrite</span>
        <span >Creates and manages structured task lists</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">WebFetch</span>
        <span >Fetches content from a specified URL</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">WebSearch</span>
        <span >Performs web searches with domain filtering</span>
      </div>
      <div class="flex items-center gap-2 border-1 p-1 rounded-lg border-gray-500">
        <span class="px-2 py-0.5 rounded font-mono text-white" style="background-color: #6A98BC;">Write</span>
        <span >Creates or overwrites files</span>
      </div>
    </div>
  </div>
</div>

<v-click>
  <div></div>
</v-click>

<style>
@keyframes pulse-border {
  0%, 100% {
    border-color: rgb(239 68 68);
    box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.5);
  }
  50% {
    border-color: rgb(239 68 68);
    box-shadow: 0 0 0 4px rgba(239, 68, 68, 0.3);
  }
}

.animate-pulse-border {
  animation: pulse-border 2s ease-in-out infinite;
  border-color: rgb(239 68 68) !important;
  border-width: 2px !important;
}
</style>

<!--
Claude Code isn't a SaaS feature – it's a **primitive**.  
You compose it like `grep | awk | sed`, but the pipes are intelligent agents you control.
-->

