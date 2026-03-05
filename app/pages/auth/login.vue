<template>
  <div
    class="min-h-screen flex items-center justify-center bg-gradient-to-br from-slate-900 via-indigo-950 to-slate-900 relative overflow-hidden"
  >
    <!-- Background Particles -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        v-for="i in 20"
        :key="i"
        class="absolute rounded-full bg-indigo-500/10"
        :style="{
          width: `${Math.random() * 6 + 2}px`,
          height: `${Math.random() * 6 + 2}px`,
          top: `${Math.random() * 100}%`,
          left: `${Math.random() * 100}%`,
          animation: `float-up ${Math.random() * 5 + 3}s ease-in-out infinite`,
          animationDelay: `${Math.random() * 3}s`,
        }"
      ></div>
    </div>

    <div class="w-full max-w-md mx-4 relative z-10">
      <!-- Logo -->
      <div class="text-center mb-10">
        <div class="inline-flex items-center gap-3 mb-6">
          <div
            class="w-14 h-14 rounded-2xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center shadow-lg shadow-indigo-500/30"
          >
            <Icon name="ph:sparkle-fill" class="text-white text-3xl" />
          </div>
        </div>
        <h1 class="text-3xl font-extrabold text-white tracking-tight">
          Welcome to AIEnglish
        </h1>
        <p class="text-indigo-200/70 mt-2 text-sm">
          Sign in to continue your AI-powered journey
        </p>
      </div>

      <!-- Login Card -->
      <div
        class="bg-white/5 backdrop-blur-xl border border-white/10 rounded-3xl p-8 shadow-2xl"
      >
        <div class="space-y-5">
          <div>
            <label
              class="block text-xs font-bold text-indigo-200/80 uppercase tracking-widest mb-2"
              >Email Address</label
            >
            <div class="relative">
              <Icon
                name="ph:envelope"
                class="absolute left-4 top-1/2 -translate-y-1/2 text-indigo-300/50 text-lg"
              />
              <input
                v-model="email"
                type="email"
                placeholder="you@example.com"
                class="w-full bg-white/5 border-2 border-white/10 rounded-xl py-3.5 pl-12 pr-4 text-white placeholder-white/30 focus:outline-none focus:border-indigo-500 focus:bg-white/10 transition-all text-sm"
              />
            </div>
          </div>
          <div>
            <label
              class="block text-xs font-bold text-indigo-200/80 uppercase tracking-widest mb-2"
              >Password</label
            >
            <div class="relative">
              <Icon
                name="ph:lock-simple"
                class="absolute left-4 top-1/2 -translate-y-1/2 text-indigo-300/50 text-lg"
              />
              <input
                v-model="password"
                :type="showPassword ? 'text' : 'password'"
                placeholder="Enter your password"
                class="w-full bg-white/5 border-2 border-white/10 rounded-xl py-3.5 pl-12 pr-12 text-white placeholder-white/30 focus:outline-none focus:border-indigo-500 focus:bg-white/10 transition-all text-sm"
              />
              <button
                @click="showPassword = !showPassword"
                class="absolute right-4 top-1/2 -translate-y-1/2 text-indigo-300/50 hover:text-indigo-300 transition"
              >
                <Icon
                  :name="showPassword ? 'ph:eye-slash' : 'ph:eye'"
                  class="text-lg"
                />
              </button>
            </div>
          </div>

          <div class="flex items-center justify-between text-sm">
            <label class="flex items-center gap-2 cursor-pointer">
              <input
                type="checkbox"
                class="w-4 h-4 rounded border-white/20 bg-white/5 text-indigo-500 focus:ring-indigo-500"
              />
              <span class="text-indigo-200/60">Remember me</span>
            </label>
            <a
              href="#"
              class="text-indigo-400 hover:text-indigo-300 font-medium transition"
              >Forgot password?</a
            >
          </div>

          <button
            @click="handleLogin"
            class="w-full py-4 rounded-xl bg-gradient-to-r from-indigo-500 to-purple-600 text-white font-bold hover:from-indigo-600 hover:to-purple-700 transition-all shadow-lg shadow-indigo-500/30 hover:shadow-indigo-500/50 hover:-translate-y-0.5 text-sm tracking-wide"
          >
            Sign In & Start Learning
          </button>
        </div>

        <!-- Divider -->
        <div class="flex items-center my-6">
          <div class="flex-1 h-px bg-white/10"></div>
          <span class="px-4 text-xs text-indigo-200/40 font-medium"
            >OR CONTINUE WITH</span
          >
          <div class="flex-1 h-px bg-white/10"></div>
        </div>

        <!-- Social Login -->
        <div class="grid grid-cols-2 gap-3">
          <button
            class="flex items-center justify-center gap-2 py-3 bg-white/5 border border-white/10 rounded-xl text-white/80 hover:bg-white/10 hover:text-white transition text-sm font-medium"
          >
            <Icon name="ph:google-logo" class="text-lg" /> Google
          </button>
          <button
            class="flex items-center justify-center gap-2 py-3 bg-white/5 border border-white/10 rounded-xl text-white/80 hover:bg-white/10 hover:text-white transition text-sm font-medium"
          >
            <Icon name="ph:github-logo" class="text-lg" /> GitHub
          </button>
        </div>

        <p class="text-center text-indigo-200/40 text-sm mt-6">
          Don't have an account?
          <NuxtLink
            to="/auth/register"
            class="text-indigo-400 hover:text-indigo-300 font-semibold transition"
            >Sign up free</NuxtLink
          >
        </p>
      </div>

      <!-- Plan Indicator -->
      <div
        class="mt-6 flex items-center justify-center gap-6 text-xs text-indigo-200/40"
      >
        <span class="flex items-center gap-1.5"
          ><Icon name="ph:check-circle-fill" class="text-emerald-400" /> Free
          Basic access</span
        >
        <span class="flex items-center gap-1.5"
          ><Icon name="ph:star-fill" class="text-amber-400" /> Premium plans
          available</span
        >
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: false });

const email = ref("");
const password = ref("");
const showPassword = ref(false);

const handleLogin = () => {
  // Simulate login → redirect to dashboard
  navigateTo("/learn/dashboard");
};
</script>
