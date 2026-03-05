<template>
  <header class="fixed top-0 w-full z-50 px-6 py-4">
    <div class="max-w-7xl mx-auto flex items-center justify-between">
      <!-- Logo + Brand -->
      <NuxtLink to="/" class="flex items-center gap-3 group">
        <div
          class="w-10 h-10 rounded-xl bg-white/10 backdrop-blur border border-white/15 flex items-center justify-center group-hover:bg-white/15 group-hover:border-white/25 transition-all duration-300 shadow-lg shadow-black/10"
        >
          <Icon
            name="ph:sparkle-fill"
            class="text-indigo-400 text-xl group-hover:text-indigo-300 transition-colors"
          />
        </div>
        <span
          class="text-lg font-extrabold text-white/90 tracking-tight group-hover:text-white transition-colors"
        >
          AIEnglish
        </span>
      </NuxtLink>

      <!-- Center Nav Pills -->
      <nav
        class="hidden md:flex items-center bg-white/5 backdrop-blur-md border border-white/10 rounded-full px-1.5 py-1.5 shadow-lg shadow-black/5"
      >
        <NuxtLink
          to="/"
          class="px-5 py-2 rounded-full text-sm font-medium text-white/50 hover:text-white hover:bg-white/10 transition-all duration-200"
        >
          Home
        </NuxtLink>
        <NuxtLink
          to="/learn"
          class="px-5 py-2 rounded-full text-sm font-medium text-white/50 hover:text-white hover:bg-white/10 transition-all duration-200"
        >
          Learn Hub
        </NuxtLink>
        <NuxtLink
          to="/learn/dashboard"
          class="px-5 py-2 rounded-full text-sm font-medium text-white/50 hover:text-white hover:bg-white/10 transition-all duration-200"
        >
          Dashboard
        </NuxtLink>
      </nav>

      <!-- Auth Actions -->
      <div class="flex items-center gap-3">
        <NuxtLink
          v-if="variant === 'login'"
          to="/auth/register"
          class="px-5 py-2.5 rounded-full text-sm font-semibold text-white/70 hover:text-white border border-white/10 hover:border-white/25 bg-white/5 hover:bg-white/10 backdrop-blur transition-all duration-200"
        >
          Create Account
        </NuxtLink>
        <NuxtLink
          v-else
          to="/auth/login"
          class="px-5 py-2.5 rounded-full text-sm font-semibold text-white/70 hover:text-white border border-white/10 hover:border-white/25 bg-white/5 hover:bg-white/10 backdrop-blur transition-all duration-200"
        >
          Sign In
        </NuxtLink>
      </div>
    </div>
  </header>
</template>

<script setup>
defineProps({
  variant: {
    type: String,
    default: "login", // 'login' or 'register'
  },
});
</script>
