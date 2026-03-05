<template>
  <div
    class="min-h-screen flex items-center justify-center bg-gradient-to-br from-slate-900 via-indigo-950 to-slate-900 relative overflow-hidden"
  >
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        v-for="i in 15"
        :key="i"
        class="absolute rounded-full bg-purple-500/10"
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
      <div class="text-center mb-10">
        <div class="inline-flex items-center gap-3 mb-6">
          <div
            class="w-14 h-14 rounded-2xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center shadow-lg shadow-indigo-500/30"
          >
            <Icon name="ph:sparkle-fill" class="text-white text-3xl" />
          </div>
        </div>
        <h1 class="text-3xl font-extrabold text-white tracking-tight">
          Create Your Account
        </h1>
        <p class="text-indigo-200/70 mt-2 text-sm">
          Join thousands of learners on AIEnglish
        </p>
      </div>

      <div
        class="bg-white/5 backdrop-blur-xl border border-white/10 rounded-3xl p-8 shadow-2xl"
      >
        <div class="space-y-5">
          <div>
            <label
              class="block text-xs font-bold text-indigo-200/80 uppercase tracking-widest mb-2"
              >Full Name</label
            >
            <div class="relative">
              <Icon
                name="ph:user"
                class="absolute left-4 top-1/2 -translate-y-1/2 text-indigo-300/50 text-lg"
              />
              <input
                v-model="name"
                type="text"
                placeholder="John Doe"
                class="w-full bg-white/5 border-2 border-white/10 rounded-xl py-3.5 pl-12 pr-4 text-white placeholder-white/30 focus:outline-none focus:border-indigo-500 focus:bg-white/10 transition-all text-sm"
              />
            </div>
          </div>
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
                type="password"
                placeholder="At least 8 characters"
                class="w-full bg-white/5 border-2 border-white/10 rounded-xl py-3.5 pl-12 pr-4 text-white placeholder-white/30 focus:outline-none focus:border-indigo-500 focus:bg-white/10 transition-all text-sm"
              />
            </div>
          </div>

          <!-- Plan Selection -->
          <div>
            <label
              class="block text-xs font-bold text-indigo-200/80 uppercase tracking-widest mb-3"
              >Choose Your Plan</label
            >
            <div class="grid grid-cols-2 gap-3">
              <button
                @click="plan = 'free'"
                :class="[
                  'p-4 rounded-xl border-2 transition-all text-left',
                  plan === 'free'
                    ? 'border-emerald-500 bg-emerald-500/10'
                    : 'border-white/10 bg-white/5 hover:bg-white/10',
                ]"
              >
                <Icon
                  name="ph:book-open"
                  class="text-xl mb-1"
                  :class="
                    plan === 'free' ? 'text-emerald-400' : 'text-white/50'
                  "
                />
                <p
                  class="text-sm font-bold"
                  :class="
                    plan === 'free' ? 'text-emerald-300' : 'text-white/70'
                  "
                >
                  Basic
                </p>
                <p
                  class="text-xs"
                  :class="
                    plan === 'free' ? 'text-emerald-300/60' : 'text-white/30'
                  "
                >
                  Free forever
                </p>
              </button>
              <button
                @click="plan = 'premium'"
                :class="[
                  'p-4 rounded-xl border-2 transition-all text-left relative overflow-hidden',
                  plan === 'premium'
                    ? 'border-indigo-500 bg-indigo-500/10'
                    : 'border-white/10 bg-white/5 hover:bg-white/10',
                ]"
              >
                <div
                  v-if="plan === 'premium'"
                  class="absolute top-0 right-0 bg-indigo-500 text-[9px] font-bold text-white px-2 py-0.5 rounded-bl-lg"
                >
                  PRO
                </div>
                <Icon
                  name="ph:crown"
                  class="text-xl mb-1"
                  :class="
                    plan === 'premium' ? 'text-indigo-400' : 'text-white/50'
                  "
                />
                <p
                  class="text-sm font-bold"
                  :class="
                    plan === 'premium' ? 'text-indigo-300' : 'text-white/70'
                  "
                >
                  Advanced
                </p>
                <p
                  class="text-xs"
                  :class="
                    plan === 'premium' ? 'text-indigo-300/60' : 'text-white/30'
                  "
                >
                  $19/month
                </p>
              </button>
            </div>
          </div>

          <button
            @click="handleRegister"
            class="w-full py-4 rounded-xl bg-gradient-to-r from-indigo-500 to-purple-600 text-white font-bold hover:from-indigo-600 hover:to-purple-700 transition-all shadow-lg shadow-indigo-500/30 hover:shadow-indigo-500/50 hover:-translate-y-0.5 text-sm tracking-wide"
          >
            Create Account
          </button>
        </div>

        <p class="text-center text-indigo-200/40 text-sm mt-6">
          Already have an account?
          <NuxtLink
            to="/auth/login"
            class="text-indigo-400 hover:text-indigo-300 font-semibold transition"
            >Sign in</NuxtLink
          >
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: false });
const name = ref("");
const email = ref("");
const password = ref("");
const plan = ref("free");

const handleRegister = () => {
  navigateTo("/learn/dashboard");
};
</script>
