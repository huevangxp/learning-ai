<template>
  <div
    class="min-h-screen bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))] from-indigo-50 via-white to-white relative overflow-hidden font-sans selection:bg-indigo-100 selection:text-indigo-900"
  >
    <!-- Auth Header (Light Theme Variant) -->

    <!-- Premium Background mesh -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        class="absolute w-[1000px] h-[1000px] rounded-full bg-indigo-500/5 blur-[120px] -top-[400px] -left-[400px] animate-pulse"
      ></div>
      <div
        class="absolute w-[800px] h-[800px] rounded-full bg-purple-500/5 blur-[100px] -bottom-[300px] -right-[300px]"
        style="animation: float-up 10s ease-in-out infinite"
      ></div>
      <!-- Subtle Grid -->
      <div
        class="absolute inset-0 opacity-[0.4]"
        style="
          background-image: radial-gradient(#6366f1 0.5px, transparent 0.5px);
          background-size: 32px 32px;
        "
      ></div>
    </div>

    <!-- Main Content -->
    <div
      class="relative z-10 flex items-center justify-center min-h-screen pt-24 pb-12 px-4"
    >
      <div class="w-full max-w-[480px]">
        <!-- Role Switching Context -->
        <div class="flex flex-col items-center mb-10">
          <div class="relative group">
            <!-- Icon Ring -->
            <div
              :class="[
                'w-20 h-20 rounded-[2.5rem] flex items-center justify-center shadow-2xl border-4 border-white transition-all duration-700 transform group-hover:rotate-12',
                role === 'admin' ? 'bg-amber-500' : 'bg-indigo-600',
              ]"
            >
              <Icon
                :name="
                  role === 'admin' ? 'ph:shield-star-fill' : 'ph:sparkle-fill'
                "
                class="text-white text-4xl"
              />
            </div>
            <!-- Floating particles around icon -->
            <div
              class="absolute -top-1 -right-1 w-4 h-4 rounded-full bg-white shadow-md flex items-center justify-center"
            >
              <div
                :class="[
                  'w-2 h-2 rounded-full animate-ping',
                  role === 'admin' ? 'bg-amber-400' : 'bg-indigo-400',
                ]"
              ></div>
            </div>
          </div>

          <h1
            class="text-4xl font-extrabold text-slate-900 tracking-tight mt-6 mb-2"
          >
            {{ role === "admin" ? "AIEnglish Admin" : "Welcome Back" }}
          </h1>
          <p class="text-slate-500 text-base font-medium">
            {{
              role === "admin"
                ? "Manage your global learning platform"
                : "Pick up exactly where you left off"
            }}
          </p>
        </div>

        <!-- Login Card -->
        <div
          class="bg-white/80 backdrop-blur-xl rounded-[2.5rem] border border-slate-200 p-10 shadow-[0_32px_64px_-16px_rgba(0,0,0,0.06)] relative overflow-hidden group"
        >
          <!-- Hover highlight -->
          <div
            class="absolute top-0 left-0 w-full h-1.5 transition-colors duration-500"
            :class="role === 'admin' ? 'bg-amber-500' : 'bg-indigo-600'"
          ></div>

          <div class="space-y-6">
            <!-- New Modern Role Tab -->
            <div
              class="bg-slate-50 p-1.5 rounded-2xl flex items-center gap-1 border border-slate-100"
            >
              <button
                @click="role = 'user'"
                :class="[
                  'flex-1 py-3 rounded-xl text-sm font-bold transition-all flex items-center justify-center gap-2',
                  role === 'user'
                    ? 'bg-indigo-600 text-white shadow-lg shadow-indigo-600/20'
                    : 'text-slate-500 hover:text-slate-800',
                ]"
              >
                <Icon name="ph:user-bold" /> Learner
              </button>
              <button
                @click="role = 'admin'"
                :class="[
                  'flex-1 py-3 rounded-xl text-sm font-bold transition-all flex items-center justify-center gap-2',
                  role === 'admin'
                    ? 'bg-amber-500 text-white shadow-lg shadow-amber-500/20'
                    : 'text-slate-500 hover:text-slate-800',
                ]"
              >
                <Icon name="ph:shield-plus-bold" /> Administrator
              </button>
            </div>

            <!-- Inputs -->
            <div class="space-y-4">
              <div class="space-y-1.5">
                <label
                  class="text-[11px] font-bold text-slate-400 uppercase tracking-widest ml-1"
                  >Identity</label
                >
                <div class="relative">
                  <span
                    class="absolute left-4 top-1/2 -translate-y-1/2 text-slate-300 pointer-events-none group-focus-within:text-indigo-500 transition-colors"
                  >
                    <Icon name="ph:at-bold" class="text-xl" />
                  </span>
                  <input
                    v-model="email"
                    type="email"
                    placeholder="Email address"
                    class="w-full bg-white border border-slate-200 rounded-2xl py-4 pl-12 pr-4 text-slate-900 placeholder:text-slate-300 focus:outline-none focus:ring-4 focus:ring-indigo-600/5 focus:border-indigo-600 transition-all text-[15px] font-medium"
                  />
                </div>
              </div>

              <div class="space-y-1.5">
                <div class="flex items-center justify-between ml-1">
                  <label
                    class="text-[11px] font-bold text-slate-400 uppercase tracking-widest"
                    >Secret</label
                  >
                  <a
                    href="#"
                    class="text-[11px] font-bold text-indigo-600 hover:text-indigo-700 uppercase tracking-widest"
                    >Forgot?</a
                  >
                </div>
                <div class="relative">
                  <span
                    class="absolute left-4 top-1/2 -translate-y-1/2 text-slate-300 pointer-events-none transition-colors"
                  >
                    <Icon name="ph:password-bold" class="text-xl" />
                  </span>
                  <input
                    v-model="password"
                    :type="showPassword ? 'text' : 'password'"
                    placeholder="Password"
                    class="w-full bg-white border border-slate-200 rounded-2xl py-4 pl-12 pr-12 text-slate-900 placeholder:text-slate-300 focus:outline-none focus:ring-4 focus:ring-indigo-600/5 focus:border-indigo-600 transition-all text-[15px] font-medium"
                  />
                  <button
                    @click="showPassword = !showPassword"
                    class="absolute right-4 top-1/2 -translate-y-1/2 text-slate-300 hover:text-slate-600 transition-colors"
                  >
                    <Icon
                      :name="showPassword ? 'ph:eye-slash' : 'ph:eye'"
                      class="text-xl"
                    />
                  </button>
                </div>
              </div>
            </div>

            <!-- Error Feedback -->
            <Transition name="fade">
              <div
                v-if="loginError"
                class="flex items-center gap-3 p-4 bg-rose-50 border border-rose-100 rounded-2xl animate-float-up"
              >
                <Icon
                  name="ph:warning-circle-fill"
                  class="text-rose-500 text-xl shrink-0"
                />
                <p class="text-rose-800 text-sm font-bold leading-tight">
                  {{ loginError }}
                </p>
              </div>
            </Transition>

            <!-- Main CTA -->
            <button
              @click="handleLogin"
              :class="[
                'w-full py-5 rounded-2xl font-black transition-all shadow-xl hover:-translate-y-1 text-base tracking-wide flex items-center justify-center gap-3 active:scale-95',
                role === 'admin'
                  ? 'bg-slate-900 text-white hover:bg-black shadow-slate-900/10'
                  : 'bg-indigo-600 text-white hover:bg-indigo-700 shadow-indigo-600/20',
              ]"
            >
              {{
                role === "admin" ? "Enter Management" : "Jump into Dashboard"
              }}
              <Icon
                name="ph:arrow-right-bold"
                class="transition-transform group-hover:translate-x-2"
              />
            </button>
          </div>

          <!-- Subtle Divider -->
          <div class="flex items-center my-8">
            <div class="flex-1 h-px bg-slate-100"></div>
            <span
              class="px-4 text-[11px] font-bold text-slate-300 uppercase tracking-widest"
              >Quick Demo Access</span
            >
            <div class="flex-1 h-px bg-slate-100"></div>
          </div>

          <!-- Shortcuts -->
          <div class="grid grid-cols-2 gap-3">
            <button
              @click="fillDemo('user')"
              class="flex items-center justify-center gap-2.5 py-3.5 px-4 rounded-2xl font-bold text-xs transition-all border border-slate-100 bg-slate-50 text-slate-600 hover:border-indigo-200 hover:bg-indigo-50 hover:text-indigo-600 group/btn"
            >
              <Icon
                name="ph:sparkle"
                class="text-lg group-hover/btn:scale-110 transition-transform"
              />
              Demo User
            </button>
            <button
              @click="fillDemo('admin')"
              class="flex items-center justify-center gap-2.5 py-3.5 px-4 rounded-2xl font-bold text-xs transition-all border border-slate-100 bg-slate-50 text-slate-600 hover:border-amber-200 hover:bg-amber-50 hover:text-amber-600 group/btn"
            >
              <Icon
                name="ph:shield-star"
                class="text-lg group-hover/btn:scale-110 transition-transform"
              />
              Demo Admin
            </button>
          </div>
        </div>

        <!-- Secondary CTA -->
        <div class="text-center mt-10">
          <p class="text-slate-500 font-medium">
            {{
              role === "admin"
                ? "Not an internal staff member?"
                : "New to the platform?"
            }}
            <NuxtLink
              to="/auth/register"
              class="text-indigo-600 font-black hover:underline underline-offset-8 decoration-2 ml-1"
            >
              {{
                role === "admin" ? "Switch to Learner" : "Create Free Account"
              }}
            </NuxtLink>
          </p>
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
const role = ref("user");
const loginError = ref("");

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
  if (!email.value || !password.value) {
    loginError.value = "Security check: Please enter both email and password.";
    return;
  }

  if (role.value === "admin") {
    if (
      email.value === demoAccounts.admin.email &&
      password.value === demoAccounts.admin.password
    ) {
      navigateTo("/admin");
    } else {
      loginError.value =
        "Invalid administrator key. Use Demo Admin for testing.";
    }
  } else {
    if (
      email.value === demoAccounts.user.email &&
      password.value === demoAccounts.user.password
    ) {
      navigateTo("/learn/dashboard");
    } else {
      loginError.value =
        "Invalid learner credentials. Use Demo User for testing.";
    }
  }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@keyframes float-up {
  0%,
  100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-30px) scale(1.05);
  }
}
</style>
