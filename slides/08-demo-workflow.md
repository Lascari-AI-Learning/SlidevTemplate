---
theme: ../
layout: default
---

<div class="text-4xl text-center mb-4 text-gray-900">Example Workflow</div>

<div class="grid grid-cols-3 gap-6 text-center">
<v-clicks>
<!-- PRIME -->
<div class="bg-gradient-to-b from-gray-50 to-gray-100 p-6 rounded-lg shadow-lg border-1 border-gray-400">
  <p class="text-3xl font-bold text-gray-900 mb-4">Prime</p>
  <div class="space-y-3 text-left text-sm">
    <div class="mb-3">
      <code class="text-xs bg-gray-200 px-2 py-1 rounded">$ claude /prime</code>
    </div>
    <ul class="space-y-2">
      <li>Reads package.json, tsconfig</li>
      <li>Run <code>tree src/</code> to see structure</li>
      <li>Loads CLAUDE.md rules</li>
      <li>Builds context graph</li>
    </ul>
    <div class="mt-3 text-xs text-green-600">
      ✓ 12 files indexed
    </div>
  </div>
</div>

<!-- PLAN -->
<div class="bg-gradient-to-b from-gray-50 to-gray-100 p-6 rounded-lg shadow-lg border-1 border-gray-400">
  <p class="text-3xl font-bold text-gray-900 mb-4">Plan</p>
  <div class="space-y-3 text-left text-sm">
    <div class="mb-3">
      <code class="text-xs bg-gray-200 px-2 py-1 rounded">"Add Stripe billing"</code>
    </div>
    <ul class="space-y-2">
      <li>Analyze existing payment code</li>
      <li>Find API patterns</li>
      <li>Check test conventions</li>
      <li>Create task breakdown</li>
    </ul>
    <div class="mt-3 text-xs text-green-600">
      ✓ 4 tasks generated
    </div>
  </div>
</div>

<!-- PRODUCE -->
<div class="bg-gradient-to-b from-gray-50 to-gray-100 p-6 rounded-lg shadow-lg border-1 border-gray-400">
  <p class="text-3xl font-bold text-gray-900 mb-4">Produce</p>
  <div class="space-y-3 text-left text-sm">
    <div class="mb-3">
      <code class="text-xs bg-gray-200 px-2 py-1 rounded">Agents execute</code>
    </div>
    <ul class="space-y-2">
      <li>Create BillingService.ts</li>
      <li>Update User model</li>
      <li class="text-red-600">✗ Tests fail - missing config</li>
      <li>Update docs with config steps</li>
    </ul>
    <div class="mt-3 text-xs text-green-600">
      ✓ Fixed & all tests passing
    </div>
  </div>
</div>
</v-clicks>
</div>

<v-click>
<div class="mt-4 bg-purple-50 p-2 rounded-lg shadow-lg border-1 border-purple-500 text-center">
  <p class="text-lg text-gray-900 font-semibold">You Controlled the Workflow ... Claude Supplied the Compute.</p>
</div>
</v-click>

<!--
This demo shows the actual Claude Code commands in action. Notice how each phase builds on the previous:

1. **Prime**: We load context once, not repeatedly
2. **Plan**: Claude understands your codebase patterns and conventions
3. **Produce**: Multiple agents work in parallel, following your standards

The key insight: You're not writing prompts, you're orchestrating intelligent agents.
-->