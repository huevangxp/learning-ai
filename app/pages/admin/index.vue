<template>
  <div>
    <div
      class="mb-8 flex flex-col md:flex-row md:items-center justify-between gap-4"
    >
      <div>
        <h2 class="text-3xl font-bold text-slate-900 tracking-tight">
          System Overview
        </h2>
        <p class="text-slate-500 mt-1">
          Monitor user activity, revenue, and AI system health metrics.
        </p>
      </div>
      <div class="flex gap-3 text-sm">
        <button
          class="px-5 py-2.5 bg-white border border-slate-200 text-slate-700 rounded-xl hover:bg-slate-50 transition shadow-sm font-medium"
        >
          Export Report
        </button>
        <button
          class="px-5 py-2.5 bg-slate-900 text-white rounded-xl hover:bg-slate-800 transition shadow-md font-medium"
        >
          Refresh Data
        </button>
      </div>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-10">
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm flex items-center justify-between hover:shadow-lg hover:-translate-y-1 transition duration-300"
      >
        <div>
          <p class="text-sm font-medium text-slate-500 mb-2">Total Users</p>
          <h3 class="text-4xl font-extrabold text-slate-900 tracking-tight">
            12,492
          </h3>
        </div>
        <div
          class="w-14 h-14 rounded-2xl bg-indigo-50 border border-indigo-100 flex items-center justify-center text-indigo-600 shadow-inner"
        >
          <Icon name="ph:users-fill" class="text-3xl" />
        </div>
      </div>
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm flex items-center justify-between hover:shadow-lg hover:-translate-y-1 transition duration-300"
      >
        <div>
          <p class="text-sm font-medium text-slate-500 mb-2">
            Active Pro Users
          </p>
          <h3 class="text-4xl font-extrabold text-slate-900 tracking-tight">
            3,812
          </h3>
        </div>
        <div
          class="w-14 h-14 rounded-2xl bg-gradient-to-br from-indigo-500 to-purple-500 border border-indigo-200 flex items-center justify-center text-white shadow-md"
        >
          <Icon name="ph:star-fill" class="text-3xl" />
        </div>
      </div>
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm flex items-center justify-between hover:shadow-lg hover:-translate-y-1 transition duration-300"
      >
        <div>
          <p class="text-sm font-medium text-slate-500 mb-2">Monthly MRR</p>
          <h3 class="text-4xl font-extrabold text-emerald-600 tracking-tight">
            $72.4k
          </h3>
        </div>
        <div
          class="w-14 h-14 rounded-2xl bg-emerald-50 border border-emerald-100 flex items-center justify-center text-emerald-600 shadow-inner"
        >
          <Icon name="ph:currency-dollar-fill" class="text-3xl" />
        </div>
      </div>
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm flex items-center justify-between hover:shadow-lg hover:-translate-y-1 transition duration-300"
      >
        <div>
          <p class="text-sm font-medium text-slate-500 mb-2">
            AI Requests Today
          </p>
          <h3 class="text-4xl font-extrabold text-slate-900 tracking-tight">
            42.1k
          </h3>
        </div>
        <div
          class="w-14 h-14 rounded-2xl bg-slate-900 border border-slate-700 flex items-center justify-center text-indigo-400 shadow-md"
        >
          <Icon name="ph:robot-fill" class="text-3xl" />
        </div>
      </div>
    </div>

    <div class="grid lg:grid-cols-3 gap-8 pb-10">
      <!-- Recent Signups -->
      <div
        class="lg:col-span-2 bg-white rounded-3xl border border-slate-200 shadow-[0_4px_20px_rgb(0,0,0,0.03)] overflow-hidden"
      >
        <div
          class="p-8 border-b border-slate-100 flex justify-between items-center bg-white"
        >
          <div>
            <h2 class="font-bold text-xl text-slate-900">Recent Signups</h2>
            <p
              class="text-sm text-slate-500 mt-1 pb-1 border-b-2 border-indigo-500 inline-block"
            >
              Last 24 hours
            </p>
          </div>
          <button
            class="text-sm bg-slate-100 text-slate-700 px-4 py-2 rounded-lg hover:bg-slate-200 font-medium transition cursor-pointer"
          >
            View All Activity
          </button>
        </div>
        <div class="overflow-x-auto">
          <table class="w-full text-left">
            <thead>
              <tr
                class="text-xs uppercase text-slate-400 font-bold tracking-wider border-b border-slate-100 bg-slate-50/50"
              >
                <th class="py-5 px-8">User Info</th>
                <th class="py-5 px-8">Subscription Plan</th>
                <th class="py-5 px-8">Status</th>
                <th class="py-5 px-8 text-right">Joined</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-100">
              <tr
                class="hover:bg-indigo-50/30 transition group"
                v-for="i in 5"
                :key="i"
              >
                <td class="py-4 px-8">
                  <div class="flex items-center gap-4">
                    <div
                      class="w-10 h-10 rounded-full bg-slate-100 flex items-center justify-center text-slate-600 text-sm font-bold border border-slate-200"
                    >
                      U{{ i }}
                    </div>
                    <div>
                      <p
                        class="font-bold text-slate-800 text-sm group-hover:text-indigo-700 transition"
                      >
                        User Identity {{ i * 42 }}
                      </p>
                      <p class="text-xs text-slate-500">
                        user{{ i }}@example.com
                      </p>
                    </div>
                  </div>
                </td>
                <td class="py-4 px-8">
                  <span
                    v-if="i % 2 === 0"
                    class="inline-flex bg-slate-100 text-slate-600 text-xs px-3 py-1.5 rounded-lg border border-slate-200 font-bold uppercase tracking-wide"
                    >BASIC FREE</span
                  >
                  <span
                    v-else
                    class="inline-flex bg-gradient-to-br from-indigo-500 to-purple-500 text-white text-xs px-3 py-1.5 rounded-lg border border-indigo-400 font-bold shadow-sm uppercase tracking-wide"
                    >ADVANCED PRO</span
                  >
                </td>
                <td class="py-4 px-8">
                  <span
                    class="inline-flex items-center gap-2 text-sm text-slate-600 font-medium bg-emerald-50 px-3 py-1.5 rounded-lg border border-emerald-100"
                  >
                    <span
                      class="w-2 h-2 rounded-full bg-emerald-500 shadow-sm shadow-emerald-200"
                    ></span>
                    Active
                  </span>
                </td>
                <td class="py-4 px-8 text-sm text-slate-500 text-right">
                  Just now
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- System Status -->
      <div
        class="bg-white rounded-3xl border border-slate-200 shadow-[0_4px_20px_rgb(0,0,0,0.03)] p-8 flex flex-col items-stretch h-full"
      >
        <h2
          class="font-bold text-xl text-slate-900 mb-8 border-b border-slate-100 pb-4"
        >
          Gemini Services Engine
        </h2>
        <div class="space-y-6 flex-1">
          <div
            class="flex items-center justify-between p-4 bg-slate-50 rounded-2xl border border-slate-100"
          >
            <div class="flex items-center gap-4">
              <div
                class="w-12 h-12 rounded-xl bg-emerald-100 text-emerald-600 flex items-center justify-center border border-emerald-200 shadow-sm"
              >
                <Icon name="ph:check-circle-fill" class="text-2xl" />
              </div>
              <div>
                <h4 class="font-bold text-slate-800 text-[15px]">
                  Text Generation (Pro)
                </h4>
                <p class="text-xs text-slate-500 mt-1">
                  Status: Fully Operational
                </p>
              </div>
            </div>
          </div>
          <div
            class="flex items-center justify-between p-4 bg-slate-50 rounded-2xl border border-slate-100"
          >
            <div class="flex items-center gap-4">
              <div
                class="w-12 h-12 rounded-xl bg-emerald-100 text-emerald-600 flex items-center justify-center border border-emerald-200 shadow-sm"
              >
                <Icon name="ph:check-circle-fill" class="text-2xl" />
              </div>
              <div>
                <h4 class="font-bold text-slate-800 text-[15px]">
                  Speech to Text Logic
                </h4>
                <p class="text-xs text-slate-500 mt-1">
                  Status: Fully Operational
                </p>
              </div>
            </div>
          </div>
          <div
            class="flex items-center justify-between p-4 bg-amber-50 rounded-2xl border border-amber-100"
          >
            <div class="flex items-center gap-4">
              <div
                class="w-12 h-12 rounded-xl bg-white text-amber-500 flex items-center justify-center border border-amber-200 shadow-sm"
              >
                <Icon name="ph:warning-circle-fill" class="text-2xl" />
              </div>
              <div>
                <h4 class="font-bold text-amber-900 text-[15px]">
                  Basic Free Chat Limits
                </h4>
                <p class="text-xs text-amber-700 mt-1">
                  High load spikes detected
                </p>
              </div>
            </div>
          </div>
        </div>
        <button
          class="mt-8 w-full py-4 bg-slate-900 text-white rounded-2xl text-sm font-bold tracking-wide hover:bg-indigo-600 transition-colors shadow-lg hover:shadow-indigo-500/20"
        >
          Analyze Full Health Logs
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: "admin",
});
</script>
