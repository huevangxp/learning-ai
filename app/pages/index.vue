<template>
  <div class="space-y-24 pb-20">
    <!-- Hero Section -->
    <section
      class="relative pt-20 pb-16 md:pt-32 md:pb-24 overflow-hidden border-b border-gray-100"
    >
      <div
        class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))] from-indigo-50 via-white to-white"
      ></div>

      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative text-center">
        <div
          class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-indigo-50 border border-indigo-100 text-indigo-700 text-sm font-semibold mb-8 shadow-sm"
        >
          <Icon name="ph:robot-fill" /> Powered by Gemini AI
        </div>
        <h1
          class="text-5xl md:text-7xl font-extrabold text-slate-900 tracking-tight mb-8"
        >
          Accelerate English with <br />
          <span
            class="text-transparent bg-clip-text bg-gradient-to-r from-indigo-600 to-purple-600"
          >
            Intelligent Conversations
          </span>
        </h1>
        <p
          class="text-xl text-slate-600 mb-10 max-w-2xl mx-auto leading-relaxed"
        >
          Experience next-generation language learning tailored to your level.
          Start with our free basic courses or upgrade to advanced AI-led
          mastery.
        </p>
        <div class="flex flex-col sm:flex-row justify-center gap-4">
          <NuxtLink
            to="/learn"
            class="px-8 py-4 rounded-full bg-slate-900 text-white font-semibold hover:bg-slate-800 transition-colors shadow-lg hover:shadow-xl hover:-translate-y-0.5 text-lg"
          >
            Start Learning for Free
          </NuxtLink>
          <NuxtLink
            to="/learn"
            class="px-8 py-4 rounded-full bg-white text-slate-900 border-2 border-slate-200 font-semibold hover:bg-slate-50 hover:border-slate-300 transition-colors shadow-sm text-lg"
          >
            Explore Levels
          </NuxtLink>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid md:grid-cols-3 gap-8">
        <div
          class="bg-white p-8 rounded-3xl border border-slate-200 shadow-sm hover:shadow-xl hover:-translate-y-1 transition duration-300"
        >
          <div
            class="w-14 h-14 bg-indigo-100 rounded-2xl flex items-center justify-center mb-6 text-indigo-600"
          >
            <Icon name="ph:brain-fill" class="text-3xl" />
          </div>
          <h3 class="text-2xl font-bold mb-3 text-slate-900">
            AI Personalization
          </h3>
          <p class="text-slate-600 leading-relaxed">
            Powered by Gemini, our AI adapts to your learning pace, correcting
            grammar and pronunciation instantly.
          </p>
        </div>
        <div
          class="bg-white p-8 rounded-3xl border border-slate-200 shadow-sm hover:shadow-xl hover:-translate-y-1 transition duration-300 relative overflow-hidden"
        >
          <div
            class="absolute top-0 right-0 bg-emerald-500 text-white text-xs font-bold px-4 py-1.5 rounded-bl-xl tracking-wider"
          >
            FREE
          </div>
          <div
            class="w-14 h-14 bg-emerald-100 rounded-2xl flex items-center justify-center mb-6 text-emerald-600"
          >
            <Icon name="ph:book-fill" class="text-3xl" />
          </div>
          <h3 class="text-2xl font-bold mb-3 text-slate-900">Basic Level</h3>
          <p class="text-slate-600 leading-relaxed">
            Master core vocabulary, essential grammar rules, and simple
            conversation starters at absolutely zero cost.
          </p>
        </div>
        <div
          class="bg-gradient-to-b from-slate-900 to-slate-800 p-8 rounded-3xl shadow-xl hover:-translate-y-1 transition duration-300 text-white relative border border-slate-700"
        >
          <div
            class="absolute top-0 right-0 bg-gradient-to-r from-indigo-500 to-purple-500 text-white text-xs font-bold px-4 py-1.5 rounded-bl-xl tracking-wider shadow-md"
          >
            PREMIUM
          </div>
          <div
            class="w-14 h-14 bg-white/10 backdrop-blur rounded-2xl flex items-center justify-center mb-6 text-indigo-300 border border-white/20"
          >
            <Icon name="ph:star-fill" class="text-3xl" />
          </div>
          <h3 class="text-2xl font-bold mb-3">Advanced Mastery</h3>
          <p class="text-slate-300 leading-relaxed">
            Unlock live mock interviews, business English contexts, and
            unlimited real-time conversational AI practice.
          </p>
        </div>
      </div>
    </section>
  </div>
</template>
