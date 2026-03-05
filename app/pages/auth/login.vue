<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-900 via-indigo-950 to-slate-900 relative overflow-hidden"
  >
    <!-- Auth Header -->
    <AuthHeader variant="login" />

    <!-- Background Mesh -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        class="absolute w-[500px] h-[500px] rounded-full bg-indigo-600/20 blur-[120px] -top-40 -left-40 animate-pulse"
      ></div>
      <div
        class="absolute w-[400px] h-[400px] rounded-full bg-purple-600/15 blur-[100px] -bottom-32 -right-32"
        style="animation: float-up 8s ease-in-out infinite"
      ></div>
      <div
        class="absolute w-[300px] h-[300px] rounded-full bg-cyan-500/10 blur-[80px] top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2"
        style="animation: float-up 6s ease-in-out infinite reverse"
      ></div>
      <div
        class="absolute inset-0 opacity-[0.03]"
        style="
          background-image: url('data:image/svg+xml,%3Csvg width=&quot;60&quot; height=&quot;60&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;%3E%3Cpath d=&quot;M60 0H0v60&quot; fill=&quot;none&quot; stroke=&quot;%23fff&quot; stroke-width=&quot;0.5&quot;/%3E%3C/svg%3E');
        "
      ></div>
      <div
        v-for="i in 25"
        :key="i"
        class="absolute rounded-full"
        :class="
          i % 3 === 0
            ? 'bg-indigo-400/20'
            : i % 3 === 1
              ? 'bg-purple-400/15'
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
              class="absolute inset-0 w-16 h-16 mx-auto rounded-2xl blur-xl"
              :class="role === 'admin' ? 'bg-amber-500/30' : 'bg-indigo-500/30'"
            ></div>
            <div
              :class="[
                'relative w-16 h-16 rounded-2xl flex items-center justify-center shadow-2xl border border-white/20 transition-all duration-500',
                role === 'admin'
                  ? 'bg-gradient-to-br from-amber-500 via-orange-500 to-red-500 shadow-amber-500/40'
                  : 'bg-gradient-to-br from-indigo-500 via-purple-500 to-indigo-600 shadow-indigo-500/40',
              ]"
            >
              <Icon
                :name="
                  role === 'admin' ? 'ph:shield-star-fill' : 'ph:sparkle-fill'
                "
                class="text-white text-3xl"
              />
            </div>
          </div>
          <h1 class="text-3xl font-extrabold text-white tracking-tight">
            {{ role === "admin" ? "Admin Portal" : "Welcome back" }}
          </h1>
          <p class="text-indigo-200/50 mt-2 text-sm font-medium">
            {{
              role === "admin"
                ? "Sign in to manage your platform"
                : "Sign in to continue your AI-powered journey"
            }}
          </p>
        </div>

        <!-- Login Card -->
        <div
          class="bg-white/[0.04] backdrop-blur-2xl border border-white/[0.08] rounded-3xl p-8 shadow-[0_8px_60px_-15px_rgba(0,0,0,0.5)] relative overflow-hidden"
        >
          <div
            class="absolute top-0 left-8 right-8 h-px bg-gradient-to-r from-transparent via-white/20 to-transparent"
          ></div>

          <div class="space-y-5">
            <!-- Role Selector -->
            <div>
              <label
                class="block text-[11px] font-bold text-indigo-200/60 uppercase tracking-[0.15em] mb-2.5"
                >Sign in as</label
              >
              <div class="grid grid-cols-2 gap-3">
                <button
                  @click="role = 'user'"
                  :class="[
                    'p-4 rounded-2xl border transition-all text-left relative overflow-hidden group',
                    role === 'user'
                      ? 'border-indigo-500/50 bg-indigo-500/[0.08]'
                      : 'border-white/[0.08] bg-white/[0.02] hover:bg-white/[0.05] hover:border-white/15',
                  ]"
                >
                  <div
                    v-if="role === 'user'"
                    class="absolute top-0 left-0 right-0 h-0.5 bg-gradient-to-r from-transparent via-indigo-400 to-transparent"
                  ></div>
                  <div class="flex items-center gap-3">
                    <div
                      class="w-10 h-10 rounded-xl flex items-center justify-center shrink-0 transition-colors"
                      :class="
                        role === 'user' ? 'bg-indigo-500/20' : 'bg-white/5'
                      "
                    >
                      <Icon
                        name="ph:student-fill"
                        class="text-xl"
                        :class="
                          role === 'user' ? 'text-indigo-400' : 'text-white/30'
                        "
                      />
                    </div>
                    <div>
                      <p
                        class="text-sm font-bold"
                        :class="
                          role === 'user' ? 'text-indigo-300' : 'text-white/60'
                        "
                      >
                        Learner
                      </p>
                      <p
                        class="text-[10px]"
                        :class="
                          role === 'user'
                            ? 'text-indigo-300/50'
                            : 'text-white/20'
                        "
                      >
                        Student account
                      </p>
                    </div>
                  </div>
                </button>
                <button
                  @click="role = 'admin'"
                  :class="[
                    'p-4 rounded-2xl border transition-all text-left relative overflow-hidden group',
                    role === 'admin'
                      ? 'border-amber-500/50 bg-amber-500/[0.08]'
                      : 'border-white/[0.08] bg-white/[0.02] hover:bg-white/[0.05] hover:border-white/15',
                  ]"
                >
                  <div
                    v-if="role === 'admin'"
                    class="absolute top-0 left-0 right-0 h-0.5 bg-gradient-to-r from-transparent via-amber-400 to-transparent"
                  ></div>
                  <div class="flex items-center gap-3">
                    <div
                      class="w-10 h-10 rounded-xl flex items-center justify-center shrink-0 transition-colors"
                      :class="
                        role === 'admin' ? 'bg-amber-500/20' : 'bg-white/5'
                      "
                    >
                      <Icon
                        name="ph:shield-star-fill"
                        class="text-xl"
                        :class="
                          role === 'admin' ? 'text-amber-400' : 'text-white/30'
                        "
                      />
                    </div>
                    <div>
                      <p
                        class="text-sm font-bold"
                        :class="
                          role === 'admin' ? 'text-amber-300' : 'text-white/60'
                        "
                      >
                        Admin
                      </p>
                      <p
                        class="text-[10px]"
                        :class="
                          role === 'admin'
                            ? 'text-amber-300/50'
                            : 'text-white/20'
                        "
                      >
                        Management portal
                      </p>
                    </div>
                  </div>
                </button>
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
                  :placeholder="
                    role === 'admin' ? 'admin@aienglish.com' : 'you@example.com'
                  "
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
                  :type="showPassword ? 'text' : 'password'"
                  placeholder="Enter your password"
                  class="w-full bg-white/[0.03] border border-white/[0.08] rounded-xl py-3.5 pl-14 pr-12 text-white placeholder-white/20 focus:outline-none focus:border-indigo-500/60 focus:bg-white/[0.06] focus:shadow-[0_0_0_4px_rgba(99,102,241,0.1)] transition-all text-sm"
                />
                <button
                  @click="showPassword = !showPassword"
                  class="absolute right-3 top-1/2 -translate-y-1/2 w-8 h-8 rounded-lg flex items-center justify-center text-white/25 hover:text-white/60 hover:bg-white/5 transition-all"
                >
                  <Icon :name="showPassword ? 'ph:eye-slash' : 'ph:eye'" />
                </button>
              </div>
            </div>

            <!-- Remember + Forgot -->
            <div class="flex items-center justify-between text-sm pt-1">
              <label class="flex items-center gap-2.5 cursor-pointer group">
                <div
                  class="w-4 h-4 rounded border border-white/15 bg-white/5 group-hover:border-white/30 transition flex items-center justify-center"
                >
                  <input type="checkbox" class="sr-only" v-model="remember" />
                  <Icon
                    v-if="remember"
                    name="ph:check-bold"
                    class="text-indigo-400 text-[10px]"
                  />
                </div>
                <span
                  class="text-white/35 group-hover:text-white/60 transition text-xs font-medium"
                  >Remember me</span
                >
              </label>
              <a
                href="#"
                class="text-indigo-400/80 hover:text-indigo-300 font-medium transition text-xs"
                >Forgot password?</a
              >
            </div>

            <!-- Error Message -->
            <div
              v-if="loginError"
              class="flex items-center gap-3 p-3 bg-red-500/10 border border-red-500/20 rounded-xl animate-float-up"
            >
              <Icon
                name="ph:warning-circle-fill"
                class="text-red-400 text-lg shrink-0"
              />
              <p class="text-red-300 text-xs font-medium">{{ loginError }}</p>
            </div>

            <!-- Submit Button -->
            <button
              @click="handleLogin"
              :class="[
                'w-full py-4 rounded-xl font-bold transition-all shadow-xl hover:-translate-y-0.5 text-sm tracking-wide relative overflow-hidden group',
                role === 'admin'
                  ? 'bg-gradient-to-r from-amber-500 to-orange-500 text-white shadow-amber-500/25 hover:shadow-amber-500/40'
                  : 'bg-gradient-to-r from-indigo-500 to-purple-600 text-white shadow-indigo-500/25 hover:shadow-indigo-500/40',
              ]"
            >
              <div
                class="absolute inset-0 bg-gradient-to-r from-white/0 via-white/10 to-white/0 translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-700"
              ></div>
              <span class="relative flex items-center justify-center gap-2">
                <Icon
                  :name="role === 'admin' ? 'ph:shield-star' : 'ph:sign-in'"
                  class="text-lg"
                />
                {{
                  role === "admin"
                    ? "Access Admin Panel"
                    : "Sign In & Start Learning"
                }}
              </span>
            </button>
          </div>

          <!-- Demo Credentials -->
          <div
            class="mt-6 p-4 bg-white/[0.03] border border-white/[0.06] rounded-2xl"
          >
            <p
              class="text-[10px] font-bold text-white/30 uppercase tracking-[0.15em] mb-3 text-center"
            >
              Quick Demo Login
            </p>
            <div class="grid grid-cols-2 gap-2">
              <button
                @click="fillDemo('user')"
                class="py-2.5 px-3 rounded-xl bg-indigo-500/10 border border-indigo-500/20 text-indigo-300 text-xs font-semibold hover:bg-indigo-500/20 transition-all flex items-center justify-center gap-1.5"
              >
                <Icon name="ph:student" /> Demo User
              </button>
              <button
                @click="fillDemo('admin')"
                class="py-2.5 px-3 rounded-xl bg-amber-500/10 border border-amber-500/20 text-amber-300 text-xs font-semibold hover:bg-amber-500/20 transition-all flex items-center justify-center gap-1.5"
              >
                <Icon name="ph:shield-star" /> Demo Admin
              </button>
            </div>
          </div>

          <!-- Divider -->
          <div class="flex items-center my-7">
            <div
              class="flex-1 h-px bg-gradient-to-r from-transparent via-white/10 to-transparent"
            ></div>
            <span
              class="px-4 text-[10px] text-white/25 font-semibold uppercase tracking-[0.2em]"
              >or continue with</span
            >
            <div
              class="flex-1 h-px bg-gradient-to-r from-transparent via-white/10 to-transparent"
            ></div>
          </div>

          <!-- Social Login -->
          <div class="grid grid-cols-2 gap-3">
            <button
              class="flex items-center justify-center gap-2.5 py-3 bg-white/[0.03] border border-white/[0.08] rounded-xl text-white/60 hover:bg-white/[0.08] hover:text-white hover:border-white/15 transition-all text-sm font-medium group"
            >
              <Icon
                name="ph:google-logo"
                class="text-lg group-hover:scale-110 transition-transform"
              />
              Google
            </button>
            <button
              class="flex items-center justify-center gap-2.5 py-3 bg-white/[0.03] border border-white/[0.08] rounded-xl text-white/60 hover:bg-white/[0.08] hover:text-white hover:border-white/15 transition-all text-sm font-medium group"
            >
              <Icon
                name="ph:github-logo"
                class="text-lg group-hover:scale-110 transition-transform"
              />
              GitHub
            </button>
          </div>

          <p class="text-center text-white/25 text-sm mt-7">
            Don't have an account?
            <NuxtLink
              to="/auth/register"
              class="text-indigo-400 hover:text-indigo-300 font-semibold transition ml-1"
              >Sign up free</NuxtLink
            >
          </p>
        </div>

        <!-- Bottom Badges -->
        <div
          class="mt-7 flex items-center justify-center gap-8 text-xs text-white/25"
        >
          <span class="flex items-center gap-2">
            <div
              class="w-5 h-5 rounded-md bg-emerald-500/20 flex items-center justify-center"
            >
              <Icon name="ph:check-bold" class="text-emerald-400 text-[10px]" />
            </div>
            Free Basic access
          </span>
          <span class="flex items-center gap-2">
            <div
              class="w-5 h-5 rounded-md bg-amber-500/20 flex items-center justify-center"
            >
              <Icon name="ph:star-fill" class="text-amber-400 text-[10px]" />
            </div>
            Premium plans available
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: false });

const email = ref("");
const password = ref("");
const showPassword = ref(false);
const remember = ref(false);
const role = ref("user");
const loginError = ref("");

// Demo credentials
const demoAccounts = {
  user: { email: "user@aienglish.com", password: "user1234" },
  admin: { email: "admin@aienglish.com", password: "admin1234" },
};

function fillDemo(type) {
  role.value = type;
  email.value = demoAccounts[type].email;
  password.value = demoAccounts[type].password;
  loginError.value = "";
}

function handleLogin() {
  loginError.value = "";

  // Validate
  if (!email.value || !password.value) {
    loginError.value = "Please enter both email and password.";
    return;
  }

  // Check credentials
  if (role.value === "admin") {
    if (
      email.value === demoAccounts.admin.email &&
      password.value === demoAccounts.admin.password
    ) {
      navigateTo("/admin");
    } else {
      loginError.value =
        "Invalid admin credentials. Try the Demo Admin button.";
    }
  } else {
    if (
      email.value === demoAccounts.user.email &&
      password.value === demoAccounts.user.password
    ) {
      navigateTo("/learn/dashboard");
    } else {
      loginError.value = "Invalid credentials. Try the Demo User button.";
    }
  }
}
</script>
