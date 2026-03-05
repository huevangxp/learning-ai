<template>
  <div
    class="h-screen flex bg-slate-50 font-sans text-slate-900 overflow-hidden selection:bg-indigo-500/30"
  >
    <aside
      class="w-72 bg-white border-r border-slate-200 flex flex-col relative z-20 shadow-sm shrink-0"
    >
      <div class="h-16 flex items-center px-6 border-b border-slate-100">
        <Icon name="ph:sparkle-fill" class="text-indigo-600 text-2xl mr-2" />
        <span
          class="font-bold text-xl bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-purple-600"
          >AIEnglish</span
        >
      </div>
      <div class="p-6 border-b border-slate-100">
        <div class="flex items-center gap-3">
          <div
            class="w-12 h-12 rounded-full bg-slate-200 overflow-hidden border-2 border-white shadow-sm shrink-0"
          >
            <img
              src="https://api.dicebear.com/7.x/avataaars/svg?seed=Felix"
              alt="User Avatar"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="overflow-hidden">
            <p class="font-bold text-sm text-slate-800 truncate">
              Student Account
            </p>
            <p
              class="text-xs text-indigo-600 font-bold bg-indigo-50 inline-block px-2 py-0.5 rounded border border-indigo-100 mt-1"
            >
              Level B1 - FREE
            </p>
          </div>
        </div>
      </div>
      <nav class="flex-1 p-4 space-y-1 overflow-y-auto custom-scrollbar">
        <NuxtLink
          to="/dashboard"
          class="flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-slate-50 text-slate-600 hover:text-indigo-600 transition font-medium text-sm"
          active-class="bg-indigo-50 text-indigo-700 font-bold border border-indigo-100 shadow-sm inner"
        >
          <Icon name="ph:squares-four-fill" class="text-xl" /> Smart Dashboard
        </NuxtLink>
        <div
          class="pt-6 pb-2 px-4 text-xs font-bold text-slate-400 uppercase tracking-wider"
        >
          Learning Labs
        </div>
        <NuxtLink
          to="/lab/speaking"
          class="flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-slate-50 text-slate-600 hover:text-indigo-600 transition font-medium text-sm"
          active-class="bg-indigo-50 text-indigo-700 font-bold border border-indigo-100 shadow-sm inner"
        >
          <Icon
            name="ph:microphone-stage-fill"
            class="text-xl text-emerald-500"
          />
          AI Speaking Lab
        </NuxtLink>
        <NuxtLink
          to="/lab/reading"
          class="flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-slate-50 text-slate-600 hover:text-indigo-600 transition font-medium text-sm"
          active-class="bg-indigo-50 text-indigo-700 font-bold border border-indigo-100 shadow-sm inner"
        >
          <Icon name="ph:book-open-text-fill" class="text-xl text-amber-500" />
          Reading & Writing
        </NuxtLink>
        <div
          class="pt-6 pb-2 px-4 text-xs font-bold text-slate-400 uppercase tracking-wider"
        >
          Assessments
        </div>
        <NuxtLink
          to="/exam"
          class="flex items-center justify-between px-4 py-3 rounded-xl hover:bg-slate-50 text-slate-600 hover:text-indigo-600 transition font-medium text-sm"
          active-class="bg-indigo-50 text-indigo-700 font-bold border border-indigo-100 shadow-sm inner"
        >
          <span class="flex items-center gap-3"
            ><Icon name="ph:medal-fill" class="text-xl text-purple-500" />
            Level-Up Exam</span
          >
          <Icon name="ph:lock-key-fill" class="text-slate-300" />
        </NuxtLink>
      </nav>
      <div class="p-6 border-t border-slate-100 bg-slate-50/50">
        <div
          class="bg-gradient-to-br from-indigo-500 to-purple-600 rounded-2xl p-5 text-white shadow-lg relative overflow-hidden group"
        >
          <div
            class="absolute -right-4 -top-4 w-20 h-20 bg-white/10 rounded-full blur-xl group-hover:bg-white/20 transition-all"
          ></div>
          <Icon
            name="ph:crown-fill"
            class="text-2xl text-amber-300 mb-2 drop-shadow-md"
          />
          <h4 class="font-bold text-[15px] mb-1">Upgrade to Premium</h4>
          <p
            class="text-[11px] text-indigo-100 mb-4 opacity-90 leading-relaxed"
          >
            Unlock unlimited Whisper API interactions.
          </p>
          <button
            class="w-full bg-white text-indigo-600 text-xs font-bold py-2.5 rounded-xl shadow-sm hover:shadow-md hover:-translate-y-0.5 transition-all"
          >
            View Plans
          </button>
        </div>
      </div>
    </aside>

    <main class="flex-1 flex flex-col relative h-screen overflow-hidden">
      <header
        class="h-16 bg-white/70 backdrop-blur-lg border-b border-slate-200/60 px-8 flex items-center justify-between z-10 sticky top-0"
      >
        <div class="flex items-center gap-4">
          <div
            class="flex items-center gap-2 bg-gradient-to-r from-orange-400 to-orange-500 text-white px-4 py-1.5 rounded-full text-xs font-bold shadow-md border border-orange-300"
          >
            <Icon
              name="ph:fire-fill"
              class="text-orange-100 text-base drop-shadow-md animate-pulse"
            />
            12 Day Streak!
          </div>
        </div>
        <div class="flex items-center gap-4">
          <button
            class="w-10 h-10 rounded-full bg-slate-100 border border-slate-200 flex items-center justify-center text-slate-500 hover:bg-white hover:shadow-sm hover:text-indigo-600 hover:border-indigo-200 transition-all disabled"
          >
            <Icon name="ph:bell-fill" class="text-lg" />
          </button>
          <NuxtLink
            to="/"
            class="text-xs font-bold text-slate-500 hover:text-slate-900 border border-slate-200 px-3 py-1.5 rounded-lg bg-white shadow-sm"
            >Logout</NuxtLink
          >
        </div>
      </header>
      <div class="flex-1 overflow-y-auto custom-scrollbar p-6 md:p-10">
        <slot />
      </div>
    </main>
  </div>
</template>
