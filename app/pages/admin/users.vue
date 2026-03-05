<template>
  <div>
    <div class="mb-8 flex items-center justify-between">
      <div>
        <h2 class="text-3xl font-extrabold text-slate-900 tracking-tight">
          Users & Billing
        </h2>
        <p class="text-slate-500 mt-1">
          Manage user subscriptions, free-tier limits, and payment tracking.
        </p>
      </div>
    </div>

    <!-- Billing Stats -->
    <div class="grid md:grid-cols-3 gap-6 mb-10">
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm flex items-center gap-5 hover:shadow-lg transition"
      >
        <div
          class="w-14 h-14 rounded-2xl bg-emerald-100 text-emerald-600 flex items-center justify-center border border-emerald-200"
        >
          <Icon name="ph:users-fill" class="text-3xl" />
        </div>
        <div>
          <p
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-0.5"
          >
            Free Users
          </p>
          <p class="text-3xl font-extrabold text-slate-900">8,680</p>
        </div>
      </div>
      <div
        class="bg-gradient-to-br from-indigo-500 to-purple-600 p-6 rounded-3xl shadow-xl text-white flex items-center gap-5 hover:scale-[1.02] transition-transform"
      >
        <div
          class="w-14 h-14 rounded-2xl bg-white/20 backdrop-blur flex items-center justify-center border border-white/30"
        >
          <Icon name="ph:crown-fill" class="text-3xl text-amber-300" />
        </div>
        <div>
          <p
            class="text-sm font-bold text-indigo-200 uppercase tracking-widest mb-0.5"
          >
            Pro Subscribers
          </p>
          <p class="text-3xl font-extrabold">3,812</p>
        </div>
      </div>
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm flex items-center gap-5 hover:shadow-lg transition"
      >
        <div
          class="w-14 h-14 rounded-2xl bg-amber-100 text-amber-600 flex items-center justify-center border border-amber-200"
        >
          <Icon name="ph:currency-dollar-fill" class="text-3xl" />
        </div>
        <div>
          <p
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-0.5"
          >
            Revenue (Month)
          </p>
          <p class="text-3xl font-extrabold text-emerald-600">$72,428</p>
        </div>
      </div>
    </div>

    <!-- Users Table -->
    <div
      class="bg-white rounded-3xl border border-slate-200 shadow-sm overflow-hidden"
    >
      <div
        class="p-6 border-b border-slate-100 flex items-center gap-4 bg-slate-50"
      >
        <div class="relative flex-1 max-w-md">
          <Icon
            name="ph:magnifying-glass"
            class="absolute left-4 top-1/2 -translate-y-1/2 text-slate-400 text-lg"
          />
          <input
            type="text"
            placeholder="Search users by name or email..."
            class="w-full bg-white border border-slate-200 rounded-xl py-3 pl-12 pr-4 text-sm focus:outline-none focus:border-indigo-500 shadow-sm text-slate-700 font-medium"
          />
        </div>
        <select
          class="bg-white border border-slate-200 rounded-xl py-3 px-4 text-sm text-slate-600 font-medium focus:outline-none focus:border-indigo-500 shadow-sm"
        >
          <option>All Plans</option>
          <option>Free Only</option>
          <option>Pro Only</option>
        </select>
      </div>

      <div class="overflow-x-auto">
        <table class="w-full text-left">
          <thead>
            <tr
              class="text-xs uppercase text-slate-400 font-bold tracking-wider border-b border-slate-100 bg-white"
            >
              <th class="py-5 px-8">User</th>
              <th class="py-5 px-8">Current Level</th>
              <th class="py-5 px-8">Subscription</th>
              <th class="py-5 px-8">AI Sessions</th>
              <th class="py-5 px-8">Progress</th>
              <th class="py-5 px-8 text-right">Actions</th>
            </tr>
          </thead>
          <tbody class="divide-y divide-slate-100">
            <tr
              v-for="user in users"
              :key="user.name"
              class="hover:bg-slate-50 transition group"
            >
              <td class="py-4 px-8">
                <div class="flex items-center gap-4">
                  <div
                    class="w-10 h-10 rounded-full flex items-center justify-center text-xs font-bold shrink-0"
                    :class="
                      user.plan === 'Pro'
                        ? 'bg-gradient-to-br from-indigo-500 to-purple-500 text-white shadow-md'
                        : 'bg-slate-100 text-slate-600 border border-slate-200'
                    "
                  >
                    {{ user.avatar }}
                  </div>
                  <div>
                    <p
                      class="font-bold text-slate-800 text-sm group-hover:text-indigo-600 transition"
                    >
                      {{ user.name }}
                    </p>
                    <p class="text-xs text-slate-500">{{ user.email }}</p>
                  </div>
                </div>
              </td>
              <td class="py-4 px-8">
                <span
                  class="inline-flex bg-slate-100 text-slate-700 text-xs px-2.5 py-1 rounded-lg font-bold border border-slate-200"
                  >{{ user.level }}</span
                >
              </td>
              <td class="py-4 px-8">
                <span
                  v-if="user.plan === 'Free'"
                  class="inline-flex bg-slate-100 text-slate-600 text-xs px-3 py-1.5 rounded-lg border border-slate-200 font-bold uppercase tracking-wide"
                  >FREE</span
                >
                <span
                  v-else
                  class="inline-flex bg-gradient-to-r from-indigo-500 to-purple-500 text-white text-xs px-3 py-1.5 rounded-lg font-bold shadow-sm uppercase tracking-wide"
                  >PRO</span
                >
              </td>
              <td class="py-4 px-8 text-sm text-slate-600 font-medium">
                {{ user.aiSessions }}
              </td>
              <td class="py-4 px-8">
                <div class="flex items-center gap-3">
                  <div
                    class="w-24 h-2 bg-slate-100 rounded-full overflow-hidden"
                  >
                    <div
                      class="h-full bg-indigo-500 rounded-full"
                      :style="{ width: user.progress + '%' }"
                    ></div>
                  </div>
                  <span class="text-xs font-bold text-slate-500"
                    >{{ user.progress }}%</span
                  >
                </div>
              </td>
              <td class="py-4 px-8 text-right">
                <button
                  class="text-sm text-indigo-600 font-semibold hover:text-indigo-800 transition"
                >
                  View
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div
        class="p-6 border-t border-slate-100 bg-white flex justify-between items-center text-sm text-slate-500"
      >
        <span>Showing 1 to {{ users.length }} of 12,492 users</span>
        <div class="flex gap-2">
          <button
            class="px-3 py-1.5 bg-slate-100 border border-slate-200 rounded-lg hover:bg-slate-200 transition font-medium"
          >
            Previous
          </button>
          <button
            class="px-3 py-1.5 bg-indigo-600 text-white rounded-lg font-medium"
          >
            1
          </button>
          <button
            class="px-3 py-1.5 bg-slate-100 border border-slate-200 rounded-lg hover:bg-slate-200 transition font-medium"
          >
            2
          </button>
          <button
            class="px-3 py-1.5 bg-slate-100 border border-slate-200 rounded-lg hover:bg-slate-200 transition font-medium"
          >
            Next
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: "admin" });

const users = ref([
  {
    name: "Sarah Kim",
    email: "sarah.k@email.com",
    avatar: "SK",
    level: "B2",
    plan: "Pro",
    aiSessions: "142",
    progress: 85,
  },
  {
    name: "Miguel Rodriguez",
    email: "miguel.r@email.com",
    avatar: "MR",
    level: "B1",
    plan: "Pro",
    aiSessions: "98",
    progress: 68,
  },
  {
    name: "John Doe",
    email: "john.d@email.com",
    avatar: "JD",
    level: "B1",
    plan: "Free",
    aiSessions: "23",
    progress: 42,
  },
  {
    name: "Yuki Tanaka",
    email: "yuki.t@email.com",
    avatar: "YT",
    level: "A2",
    plan: "Free",
    aiSessions: "15",
    progress: 31,
  },
  {
    name: "Emma Wilson",
    email: "emma.w@email.com",
    avatar: "EW",
    level: "C1",
    plan: "Pro",
    aiSessions: "256",
    progress: 92,
  },
  {
    name: "Ahmed Hassan",
    email: "ahmed.h@email.com",
    avatar: "AH",
    level: "A1",
    plan: "Free",
    aiSessions: "8",
    progress: 15,
  },
]);
</script>
