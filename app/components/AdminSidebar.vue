<template>
  <aside
    class="w-72 bg-[#0a0c10] min-h-screen text-slate-400 flex flex-col border-r border-slate-800/50 sticky top-0 h-screen shadow-2xl z-40"
  >
    <!-- Admin Logo Section -->
    <div class="h-20 flex items-center px-8 border-b border-slate-800/50 mb-4">
      <div
        class="w-10 h-10 rounded-2xl bg-indigo-600 flex items-center justify-center shadow-lg shadow-indigo-600/20 mr-3"
      >
        <Icon name="ph:sparkle-fill" class="text-white text-xl" />
      </div>
      <div>
        <p class="text-sm font-black text-white tracking-widest uppercase">
          AIEnglish
        </p>
        <p
          class="text-[10px] font-bold text-indigo-400 uppercase tracking-[0.2em] leading-none"
        >
          Admin Panel
        </p>
      </div>
    </div>

    <!-- Navigation -->
    <nav class="flex-1 px-4 space-y-2">
      <NuxtLink
        v-for="item in adminNav"
        :key="item.to"
        :to="item.to"
        class="flex items-center gap-4 px-5 py-4 rounded-2xl text-sm font-bold text-slate-500 hover:text-white group transition-all duration-300 relative overflow-hidden"
        active-class="!text-white bg-white/5 border border-white/10 shadow-inner"
        exact
      >
        <div
          :class="[
            'w-9 h-9 rounded-xl flex items-center justify-center transition-all duration-300',
            activeTo === item.to
              ? 'bg-indigo-600 text-white shadow-xl shadow-indigo-600/20'
              : 'bg-slate-800/50 text-slate-500 group-hover:bg-slate-700/50 group-hover:text-white',
          ]"
        >
          <Icon :name="item.icon" class="text-xl" />
        </div>
        <span class="flex-1 tracking-tight">{{ item.label }}</span>
        <div
          v-if="activeTo === item.to"
          class="w-1.5 h-1.5 rounded-full bg-indigo-500 shadow-[0_0_8px_rgba(99,102,241,0.6)]"
        ></div>
      </NuxtLink>
    </nav>

    <!-- Bottom User Section -->
    <div class="p-6 border-t border-slate-800/50">
      <div
        class="p-4 bg-white/5 border border-white/10 rounded-3xl flex items-center gap-3"
      >
        <div
          class="w-9 h-9 rounded-xl bg-slate-800 text-white flex items-center justify-center text-xs font-black"
        >
          AD
        </div>
        <div class="flex-1 min-w-0">
          <p class="text-xs font-black text-white truncate">Administrator</p>
          <p
            class="text-[10px] font-bold text-slate-500 uppercase tracking-tighter"
          >
            System Root
          </p>
        </div>
        <NuxtLink
          to="/"
          class="text-slate-500 hover:text-indigo-400 transition-colors"
        >
          <Icon name="ph:sign-out-bold" class="text-lg" />
        </NuxtLink>
      </div>
    </div>
  </aside>
</template>

<script setup>
const route = useRoute();
const activeTo = computed(() => route.path);

const adminNav = [
  { to: "/admin", label: "Overview", icon: "ph:squares-four-bold" },
  { to: "/admin/courses", label: "Curriculum", icon: "ph:book-bookmark-bold" },
  { to: "/admin/users", label: "Community", icon: "ph:users-bold" },
];
</script>
