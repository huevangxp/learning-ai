<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-900 via-indigo-950 to-slate-900 relative overflow-hidden"
  >
    <!-- Auth Header -->
    <AuthHeader variant="register" />

    <!-- Background Mesh -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        class="absolute w-[500px] h-[500px] rounded-full bg-purple-600/20 blur-[120px] -top-40 -right-40 animate-pulse"
      ></div>
      <div
        class="absolute w-[400px] h-[400px] rounded-full bg-indigo-600/15 blur-[100px] -bottom-32 -left-32"
        style="animation: float-up 8s ease-in-out infinite"
      ></div>
      <div
        class="absolute w-[250px] h-[250px] rounded-full bg-cyan-500/10 blur-[80px] top-1/3 left-1/3"
        style="animation: float-up 7s ease-in-out infinite reverse"
      ></div>
      <div
        class="absolute inset-0 opacity-[0.03]"
        style="
          background-image: url('data:image/svg+xml,%3Csvg width=&quot;60&quot; height=&quot;60&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;%3E%3Cpath d=&quot;M60 0H0v60&quot; fill=&quot;none&quot; stroke=&quot;%23fff&quot; stroke-width=&quot;0.5&quot;/%3E%3C/svg%3E');
        "
      ></div>
      <div
        v-for="i in 20"
        :key="i"
        class="absolute rounded-full"
        :class="
          i % 3 === 0
            ? 'bg-purple-400/20'
            : i % 3 === 1
              ? 'bg-indigo-400/15'
              : 'bg-cyan-400/10'
        "
        :style="{
          width: `${Math.random() * 4 + 1}px`,
          height: `${Math.random() * 4 + 1}px`,
          top: `${Math.random() * 100}%`,
          left: `${Math.random() * 100}%`,
          animation: `float-up ${Math.random() * 6 + 4}s ease-in-out infinite`,
          animationDelay: `${Math.random() * 4}s`,
        }"
      ></div>
    </div>

    <!-- Main Content -->
    <div
      class="relative z-10 flex items-center justify-center min-h-screen pt-20 pb-10 px-4"
    >
      <div class="w-full max-w-[440px]">
        <!-- Logo + Title -->
        <div class="text-center mb-10">
          <div class="inline-flex items-center justify-center mb-6 relative">
            <div
              class="absolute inset-0 w-16 h-16 mx-auto rounded-2xl bg-purple-500/30 blur-xl"
            ></div>
            <div
              class="relative w-16 h-16 rounded-2xl bg-gradient-to-br from-purple-500 via-indigo-500 to-purple-600 flex items-center justify-center shadow-2xl shadow-purple-500/40 border border-white/20"
            >
              <Icon name="ph:user-plus-fill" class="text-white text-3xl" />
            </div>
          </div>
          <h1 class="text-3xl font-extrabold text-white tracking-tight">
            Create your account
          </h1>
          <p class="text-indigo-200/50 mt-2 text-sm font-medium">
            Join 12,000+ learners on AIEnglish
          </p>
        </div>

        <!-- Register Card -->
        <div
          class="bg-white/[0.04] backdrop-blur-2xl border border-white/[0.08] rounded-3xl p-8 shadow-[0_8px_60px_-15px_rgba(0,0,0,0.5)] relative overflow-hidden"
        >
          <div
            class="absolute top-0 left-8 right-8 h-px bg-gradient-to-r from-transparent via-white/20 to-transparent"
          ></div>

          <div class="space-y-5">
            <!-- Full Name -->
            <div>
              <label
                class="block text-[11px] font-bold text-indigo-200/60 uppercase tracking-[0.15em] mb-2.5"
                >Full Name</label
              >
              <div class="relative group">
                <div
                  class="absolute left-4 top-1/2 -translate-y-1/2 w-8 h-8 rounded-lg bg-white/5 flex items-center justify-center group-focus-within:bg-indigo-500/20 transition-colors"
                >
                  <Icon
                    name="ph:user"
                    class="text-white/30 group-focus-within:text-indigo-400 transition-colors"
                  />
                </div>
                <input
                  v-model="name"
                  type="text"
                  placeholder="John Doe"
                  class="w-full bg-white/[0.03] border border-white/[0.08] rounded-xl py-3.5 pl-14 pr-4 text-white placeholder-white/20 focus:outline-none focus:border-indigo-500/60 focus:bg-white/[0.06] focus:shadow-[0_0_0_4px_rgba(99,102,241,0.1)] transition-all text-sm"
                />
              </div>
            </div>

            <!-- Email -->
            <div>
              <label
                class="block text-[11px] font-bold text-indigo-200/60 uppercase tracking-[0.15em] mb-2.5"
                >Email Address</label
              >
              <div class="relative group">
                <div
                  class="absolute left-4 top-1/2 -translate-y-1/2 w-8 h-8 rounded-lg bg-white/5 flex items-center justify-center group-focus-within:bg-indigo-500/20 transition-colors"
                >
                  <Icon
                    name="ph:envelope"
                    class="text-white/30 group-focus-within:text-indigo-400 transition-colors"
                  />
                </div>
                <input
                  v-model="email"
                  type="email"
                  placeholder="you@example.com"
                  class="w-full bg-white/[0.03] border border-white/[0.08] rounded-xl py-3.5 pl-14 pr-4 text-white placeholder-white/20 focus:outline-none focus:border-indigo-500/60 focus:bg-white/[0.06] focus:shadow-[0_0_0_4px_rgba(99,102,241,0.1)] transition-all text-sm"
                />
              </div>
            </div>

            <!-- Password -->
            <div>
              <label
                class="block text-[11px] font-bold text-indigo-200/60 uppercase tracking-[0.15em] mb-2.5"
                >Password</label
              >
              <div class="relative group">
                <div
                  class="absolute left-4 top-1/2 -translate-y-1/2 w-8 h-8 rounded-lg bg-white/5 flex items-center justify-center group-focus-within:bg-indigo-500/20 transition-colors"
                >
                  <Icon
                    name="ph:lock-simple"
                    class="text-white/30 group-focus-within:text-indigo-400 transition-colors"
                  />
                </div>
                <input
                  v-model="password"
                  type="password"
                  placeholder="At least 8 characters"
                  class="w-full bg-white/[0.03] border border-white/[0.08] rounded-xl py-3.5 pl-14 pr-4 text-white placeholder-white/20 focus:outline-none focus:border-indigo-500/60 focus:bg-white/[0.06] focus:shadow-[0_0_0_4px_rgba(99,102,241,0.1)] transition-all text-sm"
                />
              </div>
              <!-- Password Strength Indicator -->
              <div class="flex gap-1.5 mt-3">
                <div
                  v-for="i in 4"
                  :key="i"
                  :class="[
                    'h-1 flex-1 rounded-full transition-all duration-300',
                    password.length === 0
                      ? 'bg-white/5'
                      : password.length < 4 && i <= 1
                        ? 'bg-red-500'
                        : password.length < 8 && i <= 2
                          ? 'bg-amber-500'
                          : password.length >= 8 && i <= 3
                            ? 'bg-indigo-500'
                            : password.length >= 12
                              ? 'bg-emerald-500'
                              : 'bg-white/5',
                  ]"
                ></div>
              </div>
              <p
                class="text-[10px] font-medium mt-1.5"
                :class="
                  password.length === 0
                    ? 'text-white/15'
                    : password.length < 8
                      ? 'text-amber-400/60'
                      : 'text-emerald-400/60'
                "
              >
                {{
                  password.length === 0
                    ? "Min 8 characters"
                    : password.length < 8
                      ? `${8 - password.length} more characters needed`
                      : "Strong password ✓"
                }}
              </p>
            </div>

            <!-- Plan Selection -->
            <div>
              <label
                class="block text-[11px] font-bold text-indigo-200/60 uppercase tracking-[0.15em] mb-3"
                >Choose Your Plan</label
              >
              <div class="grid grid-cols-2 gap-3">
                <button
                  @click="plan = 'free'"
                  :class="[
                    'p-4 rounded-2xl border transition-all text-left relative overflow-hidden group',
                    plan === 'free'
                      ? 'border-emerald-500/50 bg-emerald-500/[0.08]'
                      : 'border-white/[0.08] bg-white/[0.02] hover:bg-white/[0.05] hover:border-white/15',
                  ]"
                >
                  <div
                    v-if="plan === 'free'"
                    class="absolute top-0 left-0 right-0 h-0.5 bg-gradient-to-r from-transparent via-emerald-400 to-transparent"
                  ></div>
                  <div
                    class="w-8 h-8 rounded-lg mb-2.5 flex items-center justify-center"
                    :class="
                      plan === 'free' ? 'bg-emerald-500/20' : 'bg-white/5'
                    "
                  >
                    <Icon
                      name="ph:book-open"
                      :class="
                        plan === 'free' ? 'text-emerald-400' : 'text-white/30'
                      "
                    />
                  </div>
                  <p
                    class="text-sm font-bold"
                    :class="
                      plan === 'free' ? 'text-emerald-300' : 'text-white/60'
                    "
                  >
                    Basic
                  </p>
                  <p
                    class="text-xs mt-0.5"
                    :class="
                      plan === 'free' ? 'text-emerald-300/50' : 'text-white/20'
                    "
                  >
                    Free forever
                  </p>
                </button>
                <button
                  @click="plan = 'premium'"
                  :class="[
                    'p-4 rounded-2xl border transition-all text-left relative overflow-hidden group',
                    plan === 'premium'
                      ? 'border-indigo-500/50 bg-indigo-500/[0.08]'
                      : 'border-white/[0.08] bg-white/[0.02] hover:bg-white/[0.05] hover:border-white/15',
                  ]"
                >
                  <div
                    v-if="plan === 'premium'"
                    class="absolute top-0 left-0 right-0 h-0.5 bg-gradient-to-r from-transparent via-indigo-400 to-transparent"
                  ></div>
                  <div class="absolute top-2.5 right-2.5">
                    <span
                      v-if="plan === 'premium'"
                      class="text-[8px] font-extrabold text-indigo-400 bg-indigo-500/20 px-1.5 py-0.5 rounded-md uppercase tracking-wider"
                      >Pro</span
                    >
                  </div>
                  <div
                    class="w-8 h-8 rounded-lg mb-2.5 flex items-center justify-center"
                    :class="
                      plan === 'premium' ? 'bg-indigo-500/20' : 'bg-white/5'
                    "
                  >
                    <Icon
                      name="ph:crown"
                      :class="
                        plan === 'premium' ? 'text-indigo-400' : 'text-white/30'
                      "
                    />
                  </div>
                  <p
                    class="text-sm font-bold"
                    :class="
                      plan === 'premium' ? 'text-indigo-300' : 'text-white/60'
                    "
                  >
                    Advanced
                  </p>
                  <p
                    class="text-xs mt-0.5"
                    :class="
                      plan === 'premium'
                        ? 'text-indigo-300/50'
                        : 'text-white/20'
                    "
                  >
                    $19/month
                  </p>
                </button>
              </div>
            </div>

            <!-- Submit Button -->
            <button
              @click="handleRegister"
              class="w-full py-4 rounded-xl bg-gradient-to-r from-indigo-500 to-purple-600 text-white font-bold hover:from-indigo-400 hover:to-purple-500 transition-all shadow-xl shadow-indigo-500/25 hover:shadow-indigo-500/40 hover:-translate-y-0.5 text-sm tracking-wide relative overflow-hidden group"
            >
              <div
                class="absolute inset-0 bg-gradient-to-r from-white/0 via-white/10 to-white/0 translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-700"
              ></div>
              <span class="relative">Create Account</span>
            </button>
          </div>

          <!-- Terms -->
          <p class="text-center text-white/15 text-[11px] mt-5 leading-relaxed">
            By creating an account, you agree to our
            <a
              href="#"
              class="text-white/30 hover:text-white/50 underline underline-offset-2 transition"
              >Terms of Service</a
            >
            and
            <a
              href="#"
              class="text-white/30 hover:text-white/50 underline underline-offset-2 transition"
              >Privacy Policy</a
            >
          </p>

          <p class="text-center text-white/25 text-sm mt-6">
            Already have an account?
            <NuxtLink
              to="/auth/login"
              class="text-indigo-400 hover:text-indigo-300 font-semibold transition ml-1"
              >Sign in</NuxtLink
            >
          </p>
        </div>
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
