<template>
  <div
    class="min-h-screen bg-[#f8fafc] flex font-sans text-slate-900 overflow-hidden relative"
  >
    <!-- Background Meshes -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        class="absolute w-[800px] h-[800px] rounded-full bg-indigo-500/5 blur-[120px] -top-[300px] -left-[100px] animate-pulse"
      ></div>
      <div
        class="absolute w-[600px] h-[600px] rounded-full bg-purple-500/5 blur-[100px] bottom-0 right-0 animate-pulse"
        style="animation-delay: 2s"
      ></div>
    </div>

    <!-- Connected Learning Sidebar -->
    <aside
      class="w-80 h-screen flex flex-col bg-white/80 backdrop-blur-3xl border-r border-slate-200/60 shadow-[4px_0_24px_rgba(0,0,0,0.02)] sticky top-0 z-40 transition-all duration-500"
    >
      <!-- Logo Section -->
      <div class="h-20 flex items-center px-10 border-b border-slate-200/60">
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

      <!-- User level integrated progress -->
      <div class="px-6 py-8">
        <div
          class="p-6 bg-gradient-to-br from-indigo-600/5 to-purple-600/5 rounded-[2rem] border border-indigo-100/50 relative overflow-hidden group"
        >
          <div class="relative z-10">
            <div class="flex items-center gap-4 mb-5">
              <div
                class="w-12 h-12 rounded-2xl bg-indigo-600 text-white flex items-center justify-center font-black text-lg shadow-lg shadow-indigo-600/20"
              >
                B1
              </div>
              <div>
                <p
                  class="text-[10px] font-black text-indigo-500 uppercase tracking-widest leading-none mb-1"
                >
                  Current Status
                </p>
                <p class="text-base font-black text-slate-900">Intermediate</p>
              </div>
            </div>

            <div class="space-y-2">
              <div
                class="flex items-center justify-between text-[11px] font-bold text-slate-500"
              >
                <span>{{ progressPercent }}% Mastery</span>
                <span class="text-indigo-600">680/1000 XP</span>
              </div>
              <div class="h-2 bg-slate-200 rounded-full overflow-hidden">
                <div
                  class="h-full bg-gradient-to-r from-indigo-600 to-purple-600 rounded-full transition-all duration-1000"
                  :style="{ width: progressPercent + '%' }"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Navigation System -->
      <nav class="flex-1 px-4 space-y-1.5 overflow-y-auto custom-scrollbar">
        <NuxtLink
          v-for="item in navItems"
          :key="item.to"
          :to="item.to"
          class="flex items-center gap-4 px-6 py-4 rounded-2xl text-sm font-bold text-slate-500 hover:text-indigo-600 group relative transition-all active:scale-[0.98]"
          active-class="!bg-indigo-50 !text-indigo-700"
        >
          <div
            :class="[
              'w-10 h-10 rounded-xl flex items-center justify-center transition-all duration-300',
              activeTo === item.to
                ? 'bg-white text-indigo-600 shadow-sm'
                : 'bg-transparent text-slate-400 group-hover:text-indigo-600',
            ]"
          >
            <Icon :name="item.icon" class="text-2xl" />
          </div>
          <span class="flex-1">{{ item.label }}</span>
          <div
            v-if="activeTo === item.to"
            class="absolute left-0 w-1.5 h-6 bg-indigo-600 rounded-r-full shadow-[0_0_12px_rgba(79,70,229,0.4)]"
          ></div>
          <span
            v-if="item.badge"
            class="w-2 h-2 rounded-full bg-rose-500 shadow-[0_0_8px_rgba(244,63,94,0.4)]"
          ></span>
        </NuxtLink>

        <!-- Hub Divider -->
        <div class="pt-8 pb-4">
          <p
            class="px-6 text-[10px] font-black text-slate-400 uppercase tracking-[0.2em] mb-4"
          >
            Content Library
          </p>
          <div class="space-y-1">
            <NuxtLink
              v-for="link in secondaryLinks"
              :key="link.to"
              :to="link.to"
              class="flex items-center gap-4 px-6 py-3 rounded-2xl text-sm font-bold text-slate-400 hover:text-indigo-600 hover:bg-indigo-50/50 transition-all active:scale-[0.98]"
            >
              <div
                class="w-2 h-2 rounded-full border-2 border-slate-300 group-hover:border-indigo-400 transition-colors"
              ></div>
              <span>{{ link.label }}</span>
            </NuxtLink>
          </div>
        </div>
      </nav>

      <!-- Account Integration -->
      <div class="p-6 border-t border-slate-200/60 bg-slate-50/30">
        <div class="flex items-center gap-3 p-2 group/profile cursor-pointer">
          <div
            class="w-10 h-10 rounded-2xl bg-slate-900 text-white flex items-center justify-center text-xs font-black shadow-lg shadow-black/5 group-hover/profile:rotate-3 transition-transform"
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
              class="text-[10px] font-bold text-slate-500 uppercase tracking-widest"
            >
              Free Explorer
            </p>
          </div>
          <button
            class="p-2 text-slate-400 hover:text-rose-500 transition-colors"
          >
            <Icon name="ph:sign-out-bold" class="text-xl" />
          </button>
        </div>
      </div>
    </aside>

    <!-- Content Area -->
    <div class="flex-1 flex flex-col h-screen overflow-hidden">
      <!-- Connected Glass Header -->
      <header
        class="h-20 bg-white/70 backdrop-blur-2xl border-b border-slate-200/60 flex items-center justify-between px-10 sticky top-0 z-30 shadow-[0_1px_2px_rgba(0,0,0,0.02)]"
      >
        <div class="flex items-center gap-6">
          <div class="flex flex-col">
            <h1
              class="text-xl font-black text-slate-900 tracking-tight leading-tight"
            >
              Dashboard Overview
            </h1>
            <p
              class="text-[10px] font-bold text-slate-400 uppercase tracking-[0.2em]"
            >
              {{ $route.path.split("/").pop() }} Space
            </p>
          </div>
        </div>

        <div class="flex items-center gap-5">
          <!-- Premium Streak Integration -->
          <div
            class="flex items-center gap-3 px-5 py-2.5 bg-amber-500/10 border border-amber-200/50 rounded-2xl group cursor-default"
          >
            <Icon
              name="ph:flame-fill"
              class="text-orange-500 text-xl fire-glow"
            />
            <div class="flex flex-col">
              <span class="text-xs font-black text-amber-900 tracking-tight"
                >12 DAY STREAK</span
              >
              <span class="text-[9px] font-bold text-orange-600/70 uppercase"
                >Master Rank</span
              >
            </div>
          </div>

          <!-- Modern Notifications -->
          <button
            class="relative w-12 h-12 flex items-center justify-center rounded-2xl bg-white border border-slate-200 shadow-sm text-slate-500 hover:text-indigo-600 hover:border-indigo-200 transition-all active:scale-[0.92]"
          >
            <Icon name="ph:bell-bold" class="text-xl" />
            <span
              class="absolute -top-1 -right-1 w-5 h-5 bg-rose-500 border-2 border-white rounded-full text-[10px] text-white font-black flex items-center justify-center shadow-lg shadow-rose-500/30"
              >3</span
            >
          </button>

          <!-- Profile Quick Action -->
          <div
            class="w-12 h-12 rounded-2xl bg-indigo-600 text-white flex items-center justify-center shadow-lg shadow-indigo-600/20 cursor-pointer hover:bg-indigo-700 transition-colors"
          >
            <Icon name="ph:user-bold" class="text-xl" />
          </div>
        </div>
      </header>

      <!-- Main Viewport -->
      <main class="flex-1 overflow-y-auto custom-scrollbar p-10">
        <div class="max-w-[1400px] mx-auto">
          <slot />
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const progressPercent = ref(68);

const activeTo = computed(() => route.path);

const navItems = [
  { to: "/learn/dashboard", label: "Dashboard", icon: "ph:squares-four-bold" },
  { to: "/learn/speaking", label: "Speaking Lab", icon: "ph:microphone-bold" },
  {
    to: "/learn/reading",
    label: "Core Literacy",
    icon: "ph:book-open-text-bold",
    badge: true,
  },
  { to: "/learn/exam", label: "Assessment", icon: "ph:exam-bold" },
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
