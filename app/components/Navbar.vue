<template>
  <nav
    class="fixed top-0 w-full z-50 bg-white/70 backdrop-blur-2xl border-b border-slate-200/50 shadow-[0_8px_32px_-16px_rgba(0,0,0,0.04)]"
  >
    <div class="max-w-7xl mx-auto px-6 sm:px-8">
      <div class="flex justify-between items-center h-20">
        <!-- Brand Logo -->
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
          >
            AIEnglish
          </span>
        </NuxtLink>

        <!-- Main Navigation Links -->
        <div
          class="hidden md:flex items-center bg-slate-100/50 border border-slate-200/50 rounded-2xl px-2 py-1.5"
        >
          <NuxtLink
            v-for="link in mainLinks"
            :key="link.to"
            :to="link.to"
            class="px-6 py-2 rounded-xl text-sm font-bold text-slate-500 hover:text-indigo-600 hover:bg-white transition-all duration-300"
            active-class="!text-indigo-600 bg-white shadow-sm ring-1 ring-slate-200/50"
          >
            {{ link.label }}
          </NuxtLink>
        </div>

        <!-- Auth Actions -->
        <div class="flex items-center gap-4">
          <NuxtLink
            to="/auth/login"
            class="px-6 py-2.5 rounded-2xl text-slate-600 font-bold hover:text-indigo-600 hover:bg-indigo-50 transition-all text-sm"
          >
            Sign In
          </NuxtLink>
          <NuxtLink
            to="/auth/register"
            class="px-8 py-3 rounded-2xl bg-slate-900 text-white font-black hover:bg-black hover:shadow-xl hover:shadow-slate-900/20 active:scale-95 transition-all text-sm"
          >
            Join Free
          </NuxtLink>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
const mainLinks = [
  { to: "/", label: "Home" },
  { to: "/learn", label: "Learn Hub" },
];
</script>
