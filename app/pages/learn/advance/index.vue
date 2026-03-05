<template>
  <div
    class="max-w-screen-2xl mx-auto px-4 sm:px-6 lg:px-8 py-8 h-[calc(100vh-80px)] overflow-hidden flex flex-col"
  >
    <div class="flex items-center gap-3 mb-6 shrink-0">
      <NuxtLink
        to="/learn"
        class="text-slate-500 hover:text-slate-900 transition flex items-center gap-1 text-sm font-medium"
      >
        <Icon name="ph:arrow-left" /> Back
      </NuxtLink>
      <div class="w-1 h-6 bg-slate-200"></div>
      <span
        class="bg-gradient-to-r from-indigo-500 to-purple-500 text-white text-xs font-bold px-3 py-1.5 rounded-full uppercase tracking-wider shadow-sm"
        >Advanced Mastery - Pro</span
      >
    </div>

    <div class="flex-1 flex flex-col lg:flex-row gap-6 overflow-hidden">
      <!-- AI Tutor Interface -->
      <div
        class="flex-1 bg-white rounded-3xl border border-slate-200 shadow-[0_8px_30px_rgb(0,0,0,0.04)] overflow-hidden flex flex-col relative"
      >
        <!-- Tutor Header -->
        <div
          class="h-[88px] bg-slate-900 flex items-center justify-between px-8 shrink-0 relative overflow-hidden"
        >
          <div
            class="absolute inset-0 bg-gradient-to-r from-indigo-900/50 to-purple-900/50 opacity-50 z-0"
          ></div>
          <div class="flex items-center gap-5 z-10">
            <div class="relative">
              <div
                class="w-14 h-14 rounded-full bg-gradient-to-tr from-indigo-400 to-purple-400 p-[2px] shadow-lg shadow-indigo-500/30"
              >
                <div
                  class="w-full h-full bg-slate-900 rounded-full flex items-center justify-center text-white"
                >
                  <Icon name="ph:robot-fill" class="text-3xl" />
                </div>
              </div>
              <div
                class="absolute bottom-0 right-0 w-3.5 h-3.5 bg-emerald-400 rounded-full border-[3px] border-slate-900 shrink-0"
              ></div>
            </div>
            <div>
              <h2 class="text-white font-bold text-xl tracking-tight">
                Gemini Pro Tutor
              </h2>
              <p
                class="text-indigo-200 text-sm flex items-center gap-1.5 mt-0.5"
              >
                <span class="relative flex h-2 w-2">
                  <span
                    class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"
                  ></span>
                  <span
                    class="relative inline-flex rounded-full h-2 w-2 bg-emerald-500"
                  ></span>
                </span>
                Real-time active • Matching your B2 level
              </p>
            </div>
          </div>
          <div class="flex gap-3 z-10">
            <button
              class="px-5 py-2.5 bg-white/10 text-white rounded-xl hover:bg-red-500/20 hover:text-red-300 hover:border-red-500/30 transition-all backdrop-blur text-sm font-semibold border border-white/10"
            >
              End Session
            </button>
          </div>
        </div>

        <!-- Chat Area -->
        <div class="flex-1 overflow-y-auto p-8 bg-slate-50 space-y-6">
          <div class="flex max-w-[85%]">
            <div
              class="w-10 h-10 rounded-2xl bg-indigo-100 flex items-center justify-center text-indigo-600 mr-4 shrink-0 shadow-sm border border-indigo-200"
            >
              <Icon name="ph:robot-fill" class="text-xl" />
            </div>
            <div
              class="bg-white border border-slate-200 rounded-3xl rounded-tl-sm p-5 shadow-sm text-slate-700 text-[15px] leading-relaxed"
            >
              <p>
                Welcome to your advanced business English session! Today we will
                practice a formal salary negotiation. You are the candidate, and
                I will be the hiring manager.
              </p>
              <br />
              <p class="font-semibold text-slate-900">
                Are you ready to begin? You can use your microphone or type your
                response.
              </p>
            </div>
          </div>

          <div class="flex max-w-[85%] ml-auto justify-end">
            <div
              class="bg-gradient-to-br from-indigo-600 to-purple-600 text-white rounded-3xl rounded-tr-sm p-5 shadow-md text-[15px]"
            >
              <p>Yes, I'm ready. Let's start the roleplay.</p>
            </div>
            <div
              class="w-10 h-10 rounded-2xl bg-slate-200 flex items-center justify-center text-slate-600 ml-4 shrink-0 uppercase text-xs font-bold border border-slate-300 shadow-sm"
            >
              YOU
            </div>
          </div>

          <div class="flex max-w-[85%] relative">
            <div
              class="w-10 h-10 rounded-2xl bg-indigo-100 flex items-center justify-center text-indigo-600 mr-4 shrink-0 shadow-sm border border-indigo-200"
            >
              <Icon name="ph:robot-fill" class="text-xl" />
            </div>
            <div
              class="bg-white border border-slate-200 rounded-3xl rounded-tl-sm p-5 shadow-sm text-slate-700 w-full relative group text-[15px] leading-relaxed"
            >
              <p>
                Excellent. So, we are offering $85,000 for this position. What
                are your thoughts on that figure?
              </p>
              <div class="mt-4 pt-4 border-t border-slate-100 flex gap-2">
                <span
                  class="inline-flex bg-slate-100 text-slate-600 font-medium text-xs px-3 py-1.5 rounded-lg border border-slate-200 items-center gap-1.5"
                >
                  <Icon name="ph:lightbulb-fill" class="text-amber-500" />
                  Hint: Try to anchor higher based on your market research.
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- Input Area bg-white -->
        <div class="p-6 pb-8 border-t border-slate-200 bg-white shrink-0">
          <div class="relative flex items-center max-w-4xl mx-auto">
            <button
              class="absolute left-3 w-12 h-12 flex items-center justify-center bg-slate-100 text-slate-600 hover:bg-slate-200 hover:text-indigo-600 rounded-full transition-colors shadow-sm cursor-pointer z-10 border border-slate-200"
            >
              <Icon name="ph:microphone-fill" class="text-xl" />
            </button>
            <input
              type="text"
              placeholder="Type or speak your response..."
              class="w-full bg-slate-50 border-2 border-slate-200 rounded-full py-4 pl-[72px] pr-[72px] text-slate-700 placeholder-slate-400 focus:outline-none focus:border-indigo-500 focus:bg-white shadow-inner transition-all text-[15px]"
            />
            <button
              class="absolute right-2 w-12 h-12 flex items-center justify-center bg-gradient-to-br from-indigo-500 to-purple-500 hover:from-indigo-600 hover:to-purple-600 text-white rounded-full transition-all shadow-md hover:shadow-lg hover:scale-105 z-10 cursor-pointer"
            >
              <Icon name="ph:paper-plane-right-fill" class="text-xl" />
            </button>
          </div>
        </div>
      </div>

      <!-- Live Metrics sidebar -->
      <div
        class="hidden lg:flex w-96 bg-white rounded-3xl border border-slate-200 p-8 flex-col overflow-y-auto custom-scrollbar shadow-[0_8px_30px_rgb(0,0,0,0.04)] shrink-0"
      >
        <h3
          class="font-extrabold text-slate-900 mb-8 flex items-center gap-2 text-xl"
        >
          <Icon name="ph:chart-polar-fill" class="text-indigo-500 text-2xl" />
          Session Analysis
        </h3>

        <div class="space-y-8">
          <div class="space-y-3">
            <div class="flex justify-between text-sm items-center">
              <span class="font-bold text-slate-700"
                >Pronunciation & Fluency</span
              >
              <span
                class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-0.5 rounded-full"
                >92%</span
              >
            </div>
            <div
              class="h-2.5 w-full bg-slate-100 rounded-full overflow-hidden shadow-inner"
            >
              <div
                class="h-full bg-emerald-500 rounded-full"
                style="width: 92%"
              ></div>
            </div>
          </div>

          <div class="space-y-3">
            <div class="flex justify-between text-sm items-center">
              <span class="font-bold text-slate-700">Vocabulary Level</span>
              <span
                class="bg-amber-100 text-amber-800 text-xs font-bold px-2 py-0.5 rounded-full"
                >B2 Level</span
              >
            </div>
            <div
              class="h-2.5 w-full bg-slate-100 rounded-full overflow-hidden shadow-inner"
            >
              <div
                class="h-full bg-gradient-to-r from-amber-400 to-amber-500 rounded-full"
                style="width: 75%"
              ></div>
            </div>
          </div>
        </div>

        <div
          class="mt-12 bg-indigo-50 border border-indigo-100 rounded-2xl p-6 relative"
        >
          <div
            class="absolute -top-4 left-6 bg-white rounded-full border border-indigo-100 p-1"
          >
            <div
              class="w-8 h-8 rounded-full bg-indigo-100 flex items-center justify-center text-indigo-600"
            >
              <Icon name="ph:lightbulb-fill" class="text-lg" />
            </div>
          </div>
          <h4
            class="font-bold text-slate-800 text-sm mb-3 mt-4 uppercase tracking-wider text-indigo-900"
          >
            AI Coach Feedback
          </h4>
          <div class="text-sm text-indigo-800/80 leading-relaxed space-y-3">
            <p>
              <strong class="font-bold text-indigo-900">Pro tip:</strong> To
              sound more professional in negotiation, avoid saying "I think..."
              instead try "Based on market research..."
            </p>
            <p>Your delivery speed is optimal—very clear and confident.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
