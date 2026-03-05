<template>
  <div class="min-h-screen bg-slate-50 flex font-sans text-slate-900">
    <!-- Learning Sidebar -->
    <aside
      class="w-72 bg-white min-h-screen flex flex-col border-r border-slate-200 sticky top-0 h-screen shadow-sm"
    >
      <!-- Logo -->
      <div class="h-16 flex items-center px-6 border-b border-slate-100">
        <NuxtLink to="/" class="flex items-center gap-2">
          <Icon name="ph:sparkle-fill" class="text-indigo-600 text-xl" />
          <span
            class="text-lg font-extrabold bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-purple-600 tracking-tight"
            >AIEnglish</span
          >
        </NuxtLink>
      </div>

      <!-- User Level Badge -->
      <div
        class="mx-4 mt-5 p-4 bg-gradient-to-br from-indigo-50 to-purple-50 rounded-2xl border border-indigo-100"
      >
        <div class="flex items-center gap-3">
          <div
            class="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-600 text-white flex items-center justify-center font-extrabold text-sm shadow-md"
          >
            B1
          </div>
          <div>
            <p class="text-xs font-bold text-indigo-900">Intermediate</p>
            <p class="text-[11px] text-indigo-500 font-medium">
              2,450 XP earned
            </p>
          </div>
        </div>
        <div class="mt-3 h-1.5 bg-indigo-200/50 rounded-full overflow-hidden">
          <div
            class="h-full bg-gradient-to-r from-indigo-500 to-purple-500 rounded-full"
            style="width: 68%"
          ></div>
        </div>
        <p class="text-[10px] text-indigo-500 mt-1.5 font-semibold">
          680/1000 XP to B2
        </p>
      </div>

      <!-- Navigation -->
      <nav class="flex-1 p-4 space-y-1 mt-2">
        <NuxtLink
          to="/learn/dashboard"
          class="flex items-center gap-3 px-4 py-3 rounded-xl text-sm font-medium hover:bg-slate-50 text-slate-600 hover:text-slate-900 transition"
          active-class="!bg-indigo-50 !text-indigo-700 font-semibold border border-indigo-100"
        >
          <Icon name="ph:squares-four-fill" class="text-lg" /> Dashboard
        </NuxtLink>
        <NuxtLink
          to="/learn/speaking"
          class="flex items-center gap-3 px-4 py-3 rounded-xl text-sm font-medium hover:bg-slate-50 text-slate-600 hover:text-slate-900 transition"
          active-class="!bg-indigo-50 !text-indigo-700 font-semibold border border-indigo-100"
        >
          <Icon name="ph:microphone-fill" class="text-lg" /> AI Speaking Lab
        </NuxtLink>
        <NuxtLink
          to="/learn/reading"
          class="flex items-center gap-3 px-4 py-3 rounded-xl text-sm font-medium hover:bg-slate-50 text-slate-600 hover:text-slate-900 transition"
          active-class="!bg-indigo-50 !text-indigo-700 font-semibold border border-indigo-100"
        >
          <Icon name="ph:book-open-text-fill" class="text-lg" /> Reading &
          Writing
        </NuxtLink>
        <NuxtLink
          to="/learn/exam"
          class="flex items-center gap-3 px-4 py-3 rounded-xl text-sm font-medium hover:bg-slate-50 text-slate-600 hover:text-slate-900 transition relative"
          active-class="!bg-indigo-50 !text-indigo-700 font-semibold border border-indigo-100"
        >
          <Icon name="ph:exam-fill" class="text-lg" /> Level-Up Exam
          <span
            class="ml-auto w-2 h-2 rounded-full bg-emerald-500 animate-pulse"
          ></span>
        </NuxtLink>

        <div class="!mt-6 pt-4 border-t border-slate-100">
          <p
            class="px-4 text-[10px] font-bold text-slate-400 uppercase tracking-widest mb-3"
          >
            Quick Access
          </p>
          <NuxtLink
            to="/learn/basic"
            class="flex items-center gap-3 px-4 py-2.5 rounded-xl text-sm font-medium hover:bg-slate-50 text-slate-500 hover:text-slate-800 transition"
          >
            <Icon name="ph:book" class="text-lg" /> Basic Courses
          </NuxtLink>
          <NuxtLink
            to="/learn/advance"
            class="flex items-center gap-3 px-4 py-2.5 rounded-xl text-sm font-medium hover:bg-slate-50 text-slate-500 hover:text-slate-800 transition"
          >
            <Icon name="ph:star" class="text-lg" /> Advanced Courses
          </NuxtLink>
        </div>
      </nav>

      <!-- Bottom Section -->
      <div class="p-4 border-t border-slate-100">
        <div class="flex items-center gap-3 px-3 py-2">
          <div
            class="w-9 h-9 rounded-full bg-gradient-to-br from-indigo-500 to-purple-500 text-white flex items-center justify-center text-xs font-bold shadow-md"
          >
            JD
          </div>
          <div class="flex-1 min-w-0">
            <p class="text-sm font-bold text-slate-800 truncate">John Doe</p>
            <p class="text-[11px] text-slate-400">Free Plan</p>
          </div>
          <button class="text-slate-400 hover:text-slate-600 transition">
            <Icon name="ph:sign-out" class="text-lg" />
          </button>
        </div>
      </div>
    </aside>

    <!-- Main Content -->
    <div class="flex-1 flex flex-col min-h-screen">
      <!-- Top Bar -->
      <header
        class="h-16 bg-white/80 backdrop-blur-md border-b border-slate-100 flex items-center justify-between px-8 sticky top-0 z-30"
      >
        <div class="flex items-center gap-4">
          <h1 class="text-lg font-bold text-slate-900">Learning Center</h1>
        </div>
        <div class="flex items-center gap-5">
          <!-- Streak -->
          <div
            class="flex items-center gap-2 px-4 py-2 bg-amber-50 border border-amber-100 rounded-full"
          >
            <Icon
              name="ph:flame-fill"
              class="text-orange-500 fire-glow text-lg"
            />
            <span class="text-sm font-extrabold text-amber-800"
              >12 day streak</span
            >
          </div>
          <!-- Notifications -->
          <button
            class="relative w-10 h-10 flex items-center justify-center rounded-xl bg-slate-100 text-slate-500 hover:bg-slate-200 hover:text-slate-700 transition"
          >
            <Icon name="ph:bell" class="text-lg" />
            <span
              class="absolute -top-0.5 -right-0.5 w-4 h-4 bg-red-500 rounded-full text-[9px] text-white font-bold flex items-center justify-center"
              >3</span
            >
          </button>
        </div>
      </header>

      <!-- Page Content -->
      <main class="flex-1 p-8 overflow-auto">
        <slot />
      </main>
    </div>
  </div>
</template>
