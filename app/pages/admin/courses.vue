<template>
  <div>
    <div class="mb-8 flex items-center justify-between">
      <div>
        <h2 class="text-3xl font-extrabold text-slate-900 tracking-tight">
          Course Management
        </h2>
        <p class="text-slate-500 mt-1">
          Manage learning modules, AI content prompts, and billing restrictions.
        </p>
      </div>
      <button
        class="px-5 py-3 bg-indigo-600 hover:bg-indigo-700 text-white rounded-xl shadow-lg hover:shadow-indigo-500/30 transition-all font-bold tracking-wide text-sm flex items-center gap-2"
      >
        <Icon name="ph:plus" class="text-lg" />
        Create New Course
      </button>
    </div>

    <!-- Stats summary -->
    <div class="grid md:grid-cols-3 gap-6 mb-10">
      <div class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm">
        <Icon name="ph:book-fill" class="text-3xl text-indigo-500 mb-4" />
        <p
          class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-1"
        >
          Total Courses
        </p>
        <p class="text-3xl font-extrabold text-slate-900">42</p>
      </div>
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm relative overflow-hidden"
      >
        <div
          class="absolute right-0 top-0 bottom-0 bg-emerald-50 border-l border-emerald-100 flex items-center justify-center px-6 border-l-dashed"
        >
          <span class="text-emerald-600 font-extrabold text-2xl">24</span>
        </div>
        <Icon name="ph:lock-open-fill" class="text-3xl text-emerald-500 mb-4" />
        <p
          class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-1"
        >
          Free Tier Courses
        </p>
        <p class="text-xl font-bold text-slate-700">Accessible to all users</p>
      </div>
      <div
        class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm relative overflow-hidden border-indigo-200"
      >
        <div
          class="absolute right-0 top-0 bottom-0 bg-indigo-50 border-l border-indigo-100 flex items-center justify-center px-6 border-l-dashed"
        >
          <span class="text-indigo-600 font-extrabold text-2xl">18</span>
        </div>
        <Icon name="ph:lock-key-fill" class="text-3xl text-purple-500 mb-4" />
        <p
          class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-1"
        >
          Pro Tier Courses
        </p>
        <p class="text-xl font-bold text-slate-700">Premium content only</p>
      </div>
    </div>

    <!-- Courses List -->
    <div
      class="bg-white rounded-3xl border border-slate-200 shadow-sm overflow-hidden mb-10"
    >
      <div
        class="p-6 border-b border-slate-100 bg-slate-50 flex items-center gap-4"
      >
        <div class="relative flex-1 max-w-md">
          <Icon
            name="ph:magnifying-glass"
            class="absolute left-4 top-1/2 -translate-y-1/2 text-slate-400 text-lg"
          />
          <input
            type="text"
            placeholder="Search courses or AI prompts..."
            class="w-full bg-white border border-slate-200 rounded-xl py-3 pl-12 pr-4 text-sm focus:outline-none focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500 shadow-sm text-slate-700 font-medium"
          />
        </div>
        <div class="flex gap-2">
          <button
            class="px-4 py-3 bg-white border border-slate-200 rounded-xl text-slate-600 text-sm font-semibold hover:bg-slate-50 transition shadow-sm flex items-center gap-2"
          >
            <Icon name="ph:funnel" class="text-lg" /> Filter
          </button>
        </div>
      </div>

      <div class="overflow-x-auto">
        <table class="w-full text-left">
          <thead>
            <tr
              class="text-xs uppercase text-slate-400 font-bold tracking-wider border-b border-slate-100 bg-white"
            >
              <th class="py-5 px-8">Course Details</th>
              <th class="py-5 px-8">Target Level</th>
              <th class="py-5 px-8">AI Integration Type</th>
              <th class="py-5 px-8">Tier</th>
              <th class="py-5 px-8 text-right">Actions</th>
            </tr>
          </thead>
          <tbody class="divide-y divide-slate-100">
            <tr
              class="hover:bg-slate-50 transition group"
              v-for="i in 4"
              :key="i"
            >
              <td class="py-5 px-8">
                <div class="flex items-center gap-4">
                  <div
                    class="w-12 h-12 rounded-2xl bg-slate-100 border border-slate-200 flex items-center justify-center shrink-0"
                  >
                    <Icon
                      name="ph:book-open-text-fill"
                      class="text-xl text-slate-600"
                    />
                  </div>
                  <div>
                    <h4
                      class="font-bold text-slate-800 text-[15px] group-hover:text-indigo-600 transition"
                    >
                      {{
                        i === 1
                          ? "Greetings & Intro"
                          : i === 2
                            ? "Business Meeting Mod 1"
                            : i === 3
                              ? "Salary Negotiation"
                              : "Everyday Slang"
                      }}
                    </h4>
                    <p
                      class="text-xs text-slate-500 mt-1 truncate max-w-[200px]"
                    >
                      Prompt engineering for Gemini...
                    </p>
                  </div>
                </div>
              </td>
              <td class="py-5 px-8">
                <span
                  class="inline-flex bg-slate-100 text-slate-700 text-xs px-2.5 py-1 rounded font-bold border border-slate-200"
                >
                  {{ i % 2 !== 0 ? "A1 - Beginner" : "B2 - Advanced" }}
                </span>
              </td>
              <td class="py-5 px-8">
                <div
                  class="flex items-center gap-2 text-sm text-slate-600 font-medium"
                >
                  <Icon name="ph:robot" class="text-indigo-500" />
                  {{ i % 2 !== 0 ? "Basic Q&A Chabot" : "Live Voice Roleplay" }}
                </div>
              </td>
              <td class="py-5 px-8">
                <span
                  v-if="i % 2 !== 0"
                  class="inline-flex bg-emerald-100/50 text-emerald-700 text-xs px-3 py-1.5 rounded-lg border border-emerald-200 font-bold tracking-wide"
                  >FREE TIER</span
                >
                <span
                  v-else
                  class="inline-flex bg-gradient-to-r from-indigo-500 to-purple-500 text-white text-xs px-3 py-1.5 rounded-lg font-bold tracking-wide shadow-sm"
                  >PRO TIER</span
                >
              </td>
              <td class="py-5 px-8 text-right">
                <button
                  class="w-8 h-8 rounded-full bg-slate-100 text-slate-500 hover:bg-slate-200 hover:text-indigo-600 flex items-center justify-center mx-auto transition cursor-pointer"
                >
                  <Icon name="ph:dots-three-bold" />
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div
        class="p-6 border-t border-slate-100 bg-white flex justify-end text-sm text-slate-500"
      >
        Showing 1 to 4 of 42 entries
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: "admin",
});
</script>
