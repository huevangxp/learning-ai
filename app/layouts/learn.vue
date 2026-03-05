<template>
  <div
    class="min-h-screen bg-[#f8fafc] flex font-sans text-slate-900 overflow-hidden relative"
  >
    <!-- Background Meshes for Premium Feel -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        class="absolute w-[800px] h-[800px] rounded-full bg-indigo-500/5 blur-[120px] -top-[300px] -left-[300px] animate-pulse"
      ></div>
      <div
        class="absolute w-[600px] h-[600px] rounded-full bg-purple-500/5 blur-[100px] -bottom-[200px] -right-[200px] animate-pulse"
        style="animation-delay: 2s"
      ></div>
    </div>

    <!-- Learning Sidebar (Modern Floating Card Style) -->
    <aside
      class="w-80 h-[calc(100vh-2rem)] m-4 flex flex-col bg-white/70 backdrop-blur-2xl border border-slate-200/50 rounded-[2.5rem] shadow-[0_24px_48px_-12px_rgba(0,0,0,0.04)] sticky top-4 z-40 transition-all duration-500"
    >
      <!-- Logo Section -->
      <div class="h-20 flex items-center px-10 border-b border-slate-100/50">
        <NuxtLink
          to="/"
          class="flex items-center gap-3 active:scale-95 transition-transform group"
        >
          <div
            class="w-10 h-10 rounded-2xl bg-indigo-600 flex items-center justify-center shadow-lg shadow-indigo-600/20 group-hover:rotate-12 transition-transform"
          >
            <Icon name="ph:sparkle-fill" class="text-white text-xl" />
          </div>
          <span
            class="text-xl font-black bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-purple-700 tracking-tight"
            >AIEnglish</span
          >
        </NuxtLink>
      </div>

      <!-- User Level Badge (Premium Card) -->
      <div class="px-6 py-6 border-b border-slate-100/50">
        <div
          class="p-5 bg-gradient-to-br from-indigo-600 to-purple-700 rounded-3xl shadow-xl shadow-indigo-600/20 relative overflow-hidden group"
        >
          <!-- Particle Effect -->
          <div class="absolute inset-0 opacity-20 pointer-events-none">
            <div
              class="absolute top-1 right-2 w-12 h-12 bg-white rounded-full blur-2xl animate-pulse"
            ></div>
            <div
              class="absolute bottom-1 left-2 w-8 h-8 bg-purple-400 rounded-full blur-xl animate-pulse"
              style="animation-delay: 1s"
            ></div>
          </div>

          <div class="relative z-10">
            <div class="flex items-center gap-3">
              <div
                class="w-12 h-12 rounded-2xl bg-white/20 backdrop-blur-md border border-white/20 text-white flex items-center justify-center font-black text-lg shadow-inner ring-4 ring-white/10"
              >
                B1
              </div>
              <div class="min-w-0 flex-1">
                <p
                  class="text-xs font-bold text-white/70 uppercase tracking-widest leading-none mb-1"
                >
                  Current Level
                </p>
                <p class="text-base font-black text-white truncate">
                  Intermediate
                </p>
              </div>
            </div>

            <div class="mt-5 relative">
              <div
                class="flex items-center justify-between text-[11px] font-bold text-white/80 mb-2 px-0.5"
              >
                <span>{{ progressPercent }}% Complete</span>
                <span>B2 NEXT</span>
              </div>
              <div
                class="h-2.5 bg-white/20 rounded-full overflow-hidden border border-white/10 shadow-inner"
              >
                <div
                  class="h-full bg-gradient-to-r from-white via-white to-indigo-100 rounded-full shadow-[0_0_8px_rgba(255,255,255,0.4)] transition-all duration-1000"
                  :style="{ width: progressPercent + '%' }"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Navigation System -->
      <nav class="flex-1 p-6 space-y-2 overflow-y-auto custom-scrollbar">
        <NuxtLink
          v-for="item in navItems"
          :key="item.to"
          :to="item.to"
          class="flex items-center gap-4 px-5 py-4 rounded-2xl text-sm font-bold text-slate-500 hover:text-slate-900 group relative transition-all active:scale-[0.98]"
          active-class="!bg-white !text-indigo-600 shadow-xl shadow-indigo-600/5 ring-1 ring-slate-100/50"
        >
          <div
            :class="[
              'w-9 h-9 rounded-xl flex items-center justify-center transition-all duration-300',
              activeTo === item.to
                ? 'bg-indigo-600 text-white shadow-lg shadow-indigo-600/20'
                : 'bg-slate-100 text-slate-500 group-hover:bg-indigo-100 group-hover:text-indigo-600',
            ]"
          >
            <Icon :name="item.icon" class="text-xl" />
          </div>
          <span class="flex-1">{{ item.label }}</span>
          <Icon
            v-if="activeTo === item.to"
            name="ph:caret-right-bold"
            class="text-xs opacity-50"
          />
          <span
            v-if="item.badge"
            class="w-1.5 h-1.5 rounded-full bg-rose-500 shadow-[0_0_8px_rgba(244,63,94,0.6)]"
          ></span>
        </NuxtLink>

        <!-- Quick Access Section -->
        <div class="pt-8 pb-2">
          <p
            class="px-5 text-[10px] font-black text-slate-400 uppercase tracking-[0.2em] mb-4"
          >
            Content Hub
          </p>
          <div class="space-y-1">
            <NuxtLink
              v-for="link in secondaryLinks"
              :key="link.to"
              :to="link.to"
              class="flex items-center gap-4 px-5 py-3 rounded-2xl text-sm font-bold text-slate-400 hover:text-indigo-600 hover:bg-slate-50 transition-all active:scale-[0.98]"
            >
              <div
                class="w-2 h-2 rounded-full border-2 border-slate-300 hover:border-indigo-400 transition-colors"
              ></div>
              <span>{{ link.label }}</span>
            </NuxtLink>
          </div>
        </div>
      </nav>

      <!-- Profile Section -->
      <div class="p-6">
        <div
          class="p-4 bg-slate-50/50 border border-slate-100/50 rounded-3xl flex items-center gap-3 group/profile"
        >
          <div
            class="w-10 h-10 rounded-2xl bg-gradient-to-br from-slate-800 to-black text-white flex items-center justify-center text-xs font-black shadow-lg shadow-black/10 group-hover/profile:scale-105 transition-transform"
          >
            JD
          </div>
          <div class="flex-1 min-w-0">
            <p
              class="text-sm font-black text-slate-900 truncate tracking-tight"
            >
              John Doe
            </p>
            <p
              class="text-[10px] font-bold text-slate-500 uppercase tracking-wider"
            >
              Premium Access
            </p>
          </div>
          <button
            class="w-8 h-8 rounded-xl bg-white border border-slate-100 text-slate-400 hover:text-rose-500 hover:border-rose-100 shadow-sm transition-all flex items-center justify-center group/logout"
          >
            <Icon
              name="ph:sign-out-bold"
              class="text-lg group-hover/logout:rotate-12 transition-transform"
            />
          </button>
        </div>
      </div>
    </aside>

    <!-- Main Content Area -->
    <div
      class="flex-1 flex flex-col min-h-screen relative overflow-y-auto custom-scrollbar"
    >
      <!-- Modern Glass Header -->
      <header
        class="h-20 bg-white/70 backdrop-blur-2xl border-b border-slate-200/50 flex items-center justify-between px-10 sticky top-0 z-30 shadow-[0_8px_32px_-16px_rgba(0,0,0,0.04)]"
      >
        <div class="flex items-center gap-6">
          <div class="flex flex-col">
            <h1
              class="text-xl font-black text-slate-900 tracking-tight leading-tight"
            >
              Learning Center
            </h1>
            <p
              class="text-[11px] font-bold text-slate-400 uppercase tracking-widest"
            >
              {{ $route.path.split("/").pop() }} Space
            </p>
          </div>
        </div>

        <div class="flex items-center gap-6">
          <!-- Advanced Streak Widget -->
          <div
            class="flex items-center gap-3 px-5 py-2.5 bg-gradient-to-r from-amber-50 to-orange-50 border border-amber-200/50 rounded-2xl shadow-sm hover:shadow-md transition-shadow cursor-default"
          >
            <div class="relative">
              <Icon
                name="ph:flame-fill"
                class="text-orange-500 text-xl fire-glow"
              />
              <div
                class="absolute -top-1 -right-1 w-2 h-2 rounded-full bg-orange-400 animate-ping"
              ></div>
            </div>
            <div class="flex flex-col">
              <span class="text-xs font-black text-amber-900 tracking-tight"
                >12 DAY STREAK</span
              >
              <span
                class="text-[9px] font-bold text-orange-600/70 uppercase tracking-tighter"
                >Gold Tier Status</span
              >
            </div>
          </div>

          <!-- Notification Hub -->
          <button
            class="relative w-12 h-12 flex items-center justify-center rounded-2xl bg-white border border-slate-200 shadow-sm text-slate-500 hover:bg-slate-50 hover:text-indigo-600 hover:border-indigo-100 transition-all active:scale-[0.92]"
          >
            <Icon name="ph:bell-bold" class="text-xl" />
            <span
              class="absolute -top-1 -right-1 w-5 h-5 bg-rose-500 border-2 border-white rounded-full text-[10px] text-white font-black flex items-center justify-center shadow-lg shadow-rose-500/30"
              >3</span
            >
          </button>

          <!-- Quick Action Circle -->
          <button
            class="w-12 h-12 rounded-2xl bg-slate-900 text-white flex items-center justify-center shadow-xl shadow-slate-900/20 hover:bg-black transition-colors active:scale-95"
          >
            <Icon name="ph:plus-bold" class="text-xl" />
          </button>
        </div>
      </header>

      <!-- Content Container -->
      <main class="flex-1 p-10 max-w-[1600px] mx-auto w-full">
        <slot />
      </main>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const progressPercent = ref(68);

const activeTo = computed(() => route.path);

const navItems = [
  { to: "/learn/dashboard", label: "Dashboard", icon: "ph:squares-four-fill" },
  { to: "/learn/speaking", label: "Speaking Lab", icon: "ph:microphone-fill" },
  {
    to: "/learn/reading",
    label: "Core Literacy",
    icon: "ph:book-open-text-fill",
    badge: true,
  },
  { to: "/learn/exam", label: "Assessment", icon: "ph:exam-fill" },
];

const secondaryLinks = [
  { to: "/learn/basic", label: "Foundations" },
  { to: "/learn/advance", label: "Expert Mastery" },
  { to: "/settings", label: "Preferences" },
];
</script>

<style>
.fire-glow {
  filter: drop-shadow(0 0 6px rgba(249, 115, 22, 0.4));
  animation: flicker 2s infinite ease-in-out;
}

@keyframes flicker {
  0%,
  100% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    opacity: 0.8;
    transform: scale(0.95);
  }
}

.custom-scrollbar::-webkit-scrollbar {
  width: 4px;
}
.custom-scrollbar::-webkit-scrollbar-track {
  background: transparent;
}
.custom-scrollbar::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.05);
  border-radius: 10px;
}
.custom-scrollbar:hover::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.1);
}
</style>
