---
theme: ../
layout: default
---

<div class="text-4xl text-center mb-8">The AI Coding Tool Continuum</div>

<!-- 
  Fixed duplicate attribute error: 
  There were two 'class' attributes on the div. 
  Combined all classes into a single 'class' attribute and kept the style attribute.
  This resolves the Vue compiler error and keeps the intended styling.
-->
<div class="relative mt-10 p-8 py-10 rounded-lg border-1 border-gray-500" style="background-color: #E3DACC;">
  <!-- Container for labels and line -->
  <div class="flex items-center gap-6">
    <!-- Left Label -->
    <span class="text-sm font-semibold text-rose-600 whitespace-nowrap">
      Fully <br>Autonomous <br> (Agentic)
    </span>
    <!-- Continuum Line -->
    <div class="relative h-3 bg-gradient-to-r from-rose-400 via-purple-400 to-sky-400 rounded-full shadow-lg flex-1">
    <!-- Tool Markers -->
    <!-- Devin - 5% -->
    <div class="absolute -top-8.5 left-[5%] transform -translate-x-1/2">
      <div class="bg-white px-2 py-1 rounded shadow-md text-xs font-medium">Devin, Codex, etc.</div>
      <div class="w-3 h-3 bg-rose-500 rounded-full mx-auto mt-1"></div>
    </div>
    <!-- Bolt - 10% -->
    <div class="absolute -bottom-8.5 left-[20%] transform -translate-x-1/2">
      <div class="w-3 h-3 bg-rose-500 rounded-full mx-auto mb-1"></div>
      <div class="bg-white px-2 py-1 rounded shadow-md text-xs font-medium">Bolt, Lovable, etc.</div>
    </div>
    <!-- Cursor Composer - 35% -->
    <div class="absolute -top-8.5 left-[35%] transform -translate-x-1/2">
      <div class="bg-white px-2 py-1 rounded shadow-md text-xs font-medium">Cursor, Windsurf, etc.</div>
      <div class="w-3 h-3 bg-purple-400 rounded-full mx-auto mt-1"></div>
    </div>
    <!-- Claude Code - 50% -->
    <div class="absolute -bottom-12 left-[50%] transform -translate-x-1/2">
      <div class="w-4 h-4 bg-purple-500 rounded-full mx-auto mb-1 ring-4 ring-purple-200"></div>
      <div class="bg-purple-100 px-3 py-1 rounded shadow-lg text-sm font-bold border-1 border-purple-500">Claude Code</div>
    </div>
    <!-- Aider - 85% -->
    <div class="absolute -bottom-8.5 left-[85%] transform -translate-x-1/2">
      <div class="w-3 h-3 bg-sky-500 rounded-full mx-auto mb-1"></div>
      <div class="bg-white px-2 py-1 rounded shadow-md text-xs font-medium">RepoPrompt</div>
    </div>
    <!-- RepoPrompt - 95% -->
    <div class="absolute -top-8.5 left-[95%] transform -translate-x-1/2">
      <div class="bg-white px-2 py-1 rounded shadow-md text-xs font-medium">Aider</div>
      <div class="w-3 h-3 bg-sky-400 rounded-full mx-auto mt-1"></div>
    </div>
    </div>
    <!-- Right Label -->
    <span class="text-sm font-semibold text-sky-600 whitespace-nowrap">
      Low Level<br>Control
    </span>
  </div>
</div>

  <!-- Characteristics -->
  <div class="grid grid-cols-9 gap-4 mt-8 text-xs">
    <v-click>
    <div class="col-span-2 text-center bg-gray-100 border-1 border-gray-500 p-2 px-4 rounded-lg">
      <p>Describe → Get Code</p>
      <p>Little to No Visibility</p>
      <p>Take it or Leave it</p>
    </div>
    </v-click>
    <!-- Sweet spot section - maintains layout but content is hidden until later -->
    <div class="col-span-5 items-center text-center mt-2.5">
      <v-click at="3">
      <div class="p-0.5 rounded-lg shadow-lg" style="background: linear-gradient(to right, #fb7185, #a78bfa, #38bdf8);">
        <div class="bg-white rounded-md py-4 px-2">
          <p class="text-lg mb-2 text-center">The Sweet Spot:</p>
          <p class="text-2xl font-semibold">
            <span class="text-red-600 font-bold">Agentic</span> 
            with
            <span class="text-purple-600 font-bold">Visibility</span> 
            and 
            <span class="text-sky-600 font-bold">Control</span>
          </p>
        </div>
      </div>
      </v-click>
    </div>
    <v-click at="2">
    <div class="col-span-2 text-center bg-gray-100 border-1 border-gray-500 p-2 px-4 rounded-lg">
      <p>You Drive Everything</p>
      <p>Full Transparency</p>
      <p>High Cognitive Load</p>
    </div>
    </v-click>
  </div>

<v-click at="4">
<div class="text-center mt-8">
  <p class="text-xl font-semibold">What Tool Bridges the Gap?</p>
</div>
</v-click>

<!--
This continuum represents the fundamental spectrum of AI coding tools. Every tool falls somewhere on this line, and honestly? Both extremes have their place.

## The Fully Autonomous End

Let's talk about the left side first - the fully autonomous tools. They're seductive, right? Who doesn't want to describe an app and have it magically appear?

### Pros of Full Autonomy:
- **Speed**: You can go from idea to demo in minutes
- **Accessibility**: Non-engineers can build prototypes
- **Exploration**: Great for rapid experimentation
- **Low cognitive load**: The AI handles all the complexity

### Cons of Full Autonomy:
- **Black box problem**: When it breaks (and it will), you have no idea why
- **Conference demo code**: Looks great on stage, nightmare in production
- **Quality roulette**: Sometimes brilliant, sometimes terrible, always unpredictable
- **Debugging hell**: Try explaining to your team why the AI made certain architectural choices
- **Limited customization**: Take it or leave it - no middle ground

## The Deeply Collaborative End

Now the right side - the deeply collaborative tools. These respect your expertise but...

### Pros of Deep Collaboration:
- **Full control**: Every line of code passes through your review
- **Learning opportunity**: You understand everything that's built
- **Quality assurance**: Your standards, your way
- **Debugging clarity**: You know exactly how everything works
- **Team-friendly**: Easy to explain and maintain

### Cons of Deep Collaboration:
- **You're the bottleneck**: Every decision routes through you
- **Cognitive exhaustion**: You're basically a human API orchestrating the AI
- **Limited leverage**: Not much faster than coding yourself
- **Context switching**: Constantly jumping between directing and reviewing
- **Time sink**: The review overhead can exceed the time saved

## The Reality Check

Here's what actually happens at each extreme:

With fully autonomous tools, you get what I call "drive-by architecture" - the AI makes a thousand micro-decisions you'd never make, creating technical debt before you've even shipped.

With deeply collaborative tools, you often spend more time explaining what you want than it would take to just write it yourself. It's like teaching someone to fish while you're starving.

## The Missing Middle

Neither approach is wrong. They're just optimizing for different things. But for serious engineering work - the kind where you ship to production and maintain it for years - we need something that respects both our expertise AND our time.

What if we could have the speed of autonomous execution but with the visibility and control we need as engineers? That's the sweet spot this continuum is missing.
-->

