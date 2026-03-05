<template>
  <div class="max-w-6xl mx-auto">
    <div class="mb-8">
      <h1 class="text-3xl font-extrabold text-slate-900 tracking-tight">
        Welcome back, Student!
      </h1>
      <p class="text-slate-500 mt-1 text-lg">
        Your "Daily Path" is ready. Let's reach Level B2.
      </p>
    </div>

    <div class="grid lg:grid-cols-3 gap-8">
      <div class="lg:col-span-2 space-y-8">
        <div
          class="bg-gradient-to-br from-indigo-900 via-slate-900 to-indigo-900 rounded-3xl p-8 text-white relative overflow-hidden shadow-xl border border-indigo-800/50"
        >
          <div
            class="absolute right-0 top-0 w-64 h-64 bg-indigo-500/20 rounded-full blur-3xl -translate-y-1/2 translate-x-1/4"
          ></div>
          <div
            class="flex flex-col md:flex-row md:items-center justify-between gap-6 relative z-10"
          >
            <div>
              <div
                class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-indigo-500/30 text-indigo-200 text-xs font-bold mb-4 border border-indigo-400/30"
              >
                <Icon name="ph:target-bold" /> DAILY PATH
              </div>
              <h2 class="text-3xl font-extrabold mb-2 text-white">
                Mastering Conditionals
              </h2>
              <p class="text-indigo-200 max-w-md">
                Learn how to express possibilities and hypotheticals in business
                scenarios.
              </p>
              <button
                class="mt-6 px-6 py-3 bg-white text-indigo-900 font-bold rounded-xl hover:bg-indigo-50 transition shadow-lg flex items-center gap-2"
              >
                <Icon name="ph:play-fill" /> Start Lesson (15 mins)
              </button>
            </div>

            <div
              class="relative w-32 h-32 shrink-0 flex items-center justify-center mx-auto md:mx-0"
            >
              <svg class="w-full h-full -rotate-90" viewBox="0 0 100 100">
                <circle
                  cx="50"
                  cy="50"
                  r="40"
                  stroke="rgba(255,255,255,0.1)"
                  stroke-width="8"
                  fill="none"
                />
                <circle
                  cx="50"
                  cy="50"
                  r="40"
                  stroke="#4ade80"
                  stroke-width="8"
                  fill="none"
                  stroke-dasharray="251.2"
                  stroke-dashoffset="62.8"
                  stroke-linecap="round"
                  class="transition-all duration-1000 ease-out"
                />
              </svg>
              <div
                class="absolute inset-0 flex flex-col items-center justify-center text-center"
              >
                <span class="text-2xl font-extrabold text-white">75%</span>
                <span
                  class="text-[10px] text-emerald-400 font-bold uppercase tracking-wider"
                  >To Level B2</span
                >
              </div>
            </div>
          </div>
        </div>

        <div>
          <h3
            class="font-bold text-xl text-slate-800 mb-4 flex items-center gap-2"
          >
            <Icon name="ph:flask-fill" class="text-indigo-500" /> Recommended
            Labs
          </h3>
          <div class="grid sm:grid-cols-2 gap-4">
            <NuxtLink
              to="/lab/speaking"
              class="bg-white border border-slate-200 p-6 rounded-2xl shadow-sm hover:shadow-md hover:border-emerald-200 transition group cursor-pointer"
            >
              <div
                class="w-12 h-12 bg-emerald-100 text-emerald-600 rounded-xl flex items-center justify-center mb-4 group-hover:scale-110 transition shrink-0"
              >
                <Icon name="ph:microphone-stage-fill" class="text-2xl" />
              </div>
              <h4 class="font-bold text-lg text-slate-800 mb-1">
                Speaking Practice
              </h4>
              <p class="text-sm text-slate-500">
                Live conversation simulation with AI Buddy.
              </p>
            </NuxtLink>
            <NuxtLink
              to="/lab/reading"
              class="bg-white border border-slate-200 p-6 rounded-2xl shadow-sm hover:shadow-md hover:border-amber-200 transition group cursor-pointer"
            >
              <div
                class="w-12 h-12 bg-amber-100 text-amber-600 rounded-xl flex items-center justify-center mb-4 group-hover:scale-110 transition shrink-0"
              >
                <Icon name="ph:book-open-text-fill" class="text-2xl" />
              </div>
              <h4 class="font-bold text-lg text-slate-800 mb-1">
                Reading & Writing
              </h4>
              <p class="text-sm text-slate-500">
                Interactive story comprehension.
              </p>
            </NuxtLink>
          </div>
        </div>
      </div>

      <div class="space-y-6">
        <div class="bg-white border border-slate-200 rounded-3xl p-6 shadow-sm">
          <h3 class="font-bold text-slate-800 mb-6 text-center">
            Your Skill Radar
          </h3>
          <div
            class="relative w-full aspect-square flex items-center justify-center max-w-[240px] mx-auto"
          >
            <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow-md">
              <polygon
                points="50,5 95,35 75,85 25,85 5,35"
                fill="none"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <polygon
                points="50,20 80,42 67,75 33,75 20,42"
                fill="none"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <polygon
                points="50,35 65,49 58,65 42,65 35,49"
                fill="none"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <line
                x1="50"
                y1="50"
                x2="50"
                y2="5"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <line
                x1="50"
                y1="50"
                x2="95"
                y2="35"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <line
                x1="50"
                y1="50"
                x2="75"
                y2="85"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <line
                x1="50"
                y1="50"
                x2="25"
                y2="85"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <line
                x1="50"
                y1="50"
                x2="5"
                y2="35"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <polygon
                points="50,15 85,38 60,70 35,55 15,35"
                fill="rgba(99, 102, 241, 0.4)"
                stroke="#6366f1"
                stroke-width="2"
                stroke-linejoin="round"
              />
              <circle cx="50" cy="15" r="2" fill="#4f46e5" />
              <circle cx="85" cy="38" r="2" fill="#4f46e5" />
              <circle cx="60" cy="70" r="2" fill="#4f46e5" />
              <circle cx="35" cy="55" r="2" fill="#4f46e5" />
              <circle cx="15" cy="35" r="2" fill="#4f46e5" />
            </svg>
            <div
              class="absolute top-0 inset-x-0 text-center text-[10px] font-bold text-slate-500 -mt-2"
            >
              Vocabulary
            </div>
            <div
              class="absolute top-[30%] -right-4 text-[10px] font-bold text-slate-500"
            >
              Speaking
            </div>
            <div
              class="absolute bottom-[10%] right-0 text-[10px] font-bold text-slate-500"
            >
              Listening
            </div>
            <div
              class="absolute bottom-[10%] left-0 text-[10px] font-bold text-slate-500"
            >
              Grammar
            </div>
            <div
              class="absolute top-[30%] -left-2 text-[10px] font-bold text-slate-500"
            >
              Reading
            </div>
          </div>
        </div>

        <div
          class="bg-gradient-to-br from-purple-50 to-indigo-50 border border-purple-100 rounded-3xl p-6 shadow-sm text-center"
        >
          <div
            class="w-16 h-16 bg-purple-100 text-purple-600 rounded-full flex items-center justify-center mx-auto mb-4 relative"
          >
            <div
              class="absolute inset-0 bg-purple-400 rounded-full animate-ping opacity-20"
            ></div>
            <Icon name="ph:lock-key-fill" class="text-3xl" />
          </div>
          <h4 class="font-bold text-slate-800 text-lg mb-2">
            B2 Level Up Exam
          </h4>
          <p class="text-sm text-slate-600 mb-4">
            Complete 3 more daily paths to unlock your certification exam.
          </p>
          <div class="w-full h-2.5 bg-purple-200 rounded-full overflow-hidden">
            <div class="h-full bg-purple-500 rounded-full w-[85%]"></div>
          </div>
          <div class="text-right text-xs text-purple-700 font-bold mt-2">
            85% Complete
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: "workspace",
});
</script>
