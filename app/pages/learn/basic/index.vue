<template>
  <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
    <div class="flex items-center gap-3 mb-8">
      <NuxtLink
        to="/learn"
        class="text-slate-500 hover:text-slate-900 transition flex items-center gap-1 text-sm font-medium"
      >
        <Icon name="ph:arrow-left" /> Back
      </NuxtLink>
      <div class="w-1 h-6 bg-slate-200"></div>
      <span
        class="bg-emerald-100 text-emerald-700 text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wider"
        >BASIC - FREE</span
      >
    </div>

    <div class="flex flex-col md:flex-row gap-8">
      <!-- Lesson Content -->
      <div
        class="flex-1 bg-white rounded-3xl border border-slate-200 p-8 shadow-sm"
      >
        <h1 class="text-3xl font-extrabold text-slate-900 mb-3">
          Lesson 1: Greetings & Introductions
        </h1>
        <p class="text-slate-500 mb-8 pb-6 border-b border-slate-100 text-lg">
          Learn how to say hello and introduce yourself in everyday situations.
        </p>

        <div class="space-y-6">
          <div
            class="bg-slate-50 hover:bg-white p-6 rounded-2xl border border-slate-100 hover:border-indigo-100 shadow-sm hover:shadow-md transition-all cursor-pointer"
          >
            <div class="flex gap-4 items-start">
              <div
                class="w-12 h-12 rounded-full bg-indigo-100 text-indigo-600 flex items-center justify-center shrink-0"
              >
                <Icon name="ph:speaker-high-fill" class="text-2xl" />
              </div>
              <div>
                <h3 class="font-bold text-xl text-slate-800">
                  Hello, how are you?
                </h3>
                <p class="text-slate-600 mt-1">
                  Used as a formal or semi-formal greeting.
                </p>
              </div>
            </div>
          </div>
          <div
            class="bg-slate-50 hover:bg-white p-6 rounded-2xl border border-slate-100 hover:border-indigo-100 shadow-sm hover:shadow-md transition-all cursor-pointer"
          >
            <div class="flex gap-4 items-start">
              <div
                class="w-12 h-12 rounded-full bg-indigo-100 text-indigo-600 flex items-center justify-center shrink-0"
              >
                <Icon name="ph:speaker-high-fill" class="text-2xl" />
              </div>
              <div>
                <h3 class="font-bold text-xl text-slate-800">
                  I'm fine, thank you. And you?
                </h3>
                <p class="text-slate-600 mt-1">The classic polite response.</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Mini AI Chat (Limited) -->
      <div
        class="md:w-[400px] bg-slate-900 rounded-3xl border border-slate-800 p-6 shadow-2xl flex flex-col text-white h-[600px] sticky top-24"
      >
        <div
          class="flex items-center gap-4 mb-6 pb-6 border-b border-slate-800"
        >
          <div
            class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-indigo-500 to-purple-500 text-white flex items-center justify-center shadow-lg"
          >
            <Icon name="ph:robot-fill" class="text-2xl" />
          </div>
          <div>
            <h3 class="font-bold text-lg">Gemini Basic Assistant</h3>
            <p class="text-xs text-indigo-200 mt-0.5">
              Basic Conversational Practice
            </p>
          </div>
        </div>

        <div
          class="flex-1 overflow-y-auto space-y-4 mb-4 pr-2 custom-scrollbar"
        >
          <div
            class="bg-slate-800 border border-slate-700 p-4 rounded-2xl rounded-tl-sm text-slate-100 text-sm shadow-sm leading-relaxed"
          >
            Hi! Let's practice saying hello. Try asking me how I am doing today.
          </div>
        </div>

        <div class="mt-auto relative">
          <input
            type="text"
            placeholder="Type your message..."
            class="w-full bg-slate-800 border-2 border-slate-700 rounded-2xl py-4 px-5 text-sm text-white placeholder-slate-400 focus:outline-none focus:border-indigo-500 focus:bg-slate-900 transition-colors shadow-inner"
          />
          <button
            class="absolute right-2 top-2 bottom-2 bg-indigo-500 hover:bg-indigo-400 text-white w-10 flex items-center justify-center rounded-xl transition-colors"
          >
            <Icon name="ph:paper-plane-right-fill" class="text-lg" />
          </button>
        </div>
        <div class="text-center mt-4 pb-2 text-xs text-slate-400 font-medium">
          Free daily limit: 5 messages remaining
        </div>
      </div>
    </div>
  </div>
</template>
