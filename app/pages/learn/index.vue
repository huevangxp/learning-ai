<template>
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <div class="text-center mb-16">
      <h1 class="text-4xl font-extrabold text-slate-900 mb-4">
        Choose Your Learning Path
      </h1>
      <p class="text-lg text-slate-600 max-w-2xl mx-auto">
        Select the program that best fits your goals. Start free and upgrade
        when you're ready to communicate like a native.
      </p>
    </div>

    <div class="grid md:grid-cols-2 gap-10 max-w-5xl mx-auto">
      <!-- Basic Plan -->
      <div
        class="bg-white rounded-3xl border border-slate-200 p-8 shadow-sm hover:shadow-xl transition-all flex flex-col"
      >
        <div class="mb-8">
          <span
            class="bg-emerald-100 text-emerald-700 text-sm font-bold px-3 py-1 rounded-full"
            >100% FREE</span
          >
          <h2 class="text-3xl font-bold mt-6 mb-2 text-slate-900">
            Basic Level
          </h2>
          <p class="text-slate-500">
            Perfect for beginners wanting to build a foundation.
          </p>
        </div>

        <ul class="space-y-4 mb-8 flex-1">
          <li class="flex items-start gap-3 text-slate-700">
            <Icon
              name="ph:check-circle-fill"
              class="text-emerald-500 text-xl mt-0.5"
            />
            <span>Interactive vocabulary flashcards</span>
          </li>
          <li class="flex items-start gap-3 text-slate-700">
            <Icon
              name="ph:check-circle-fill"
              class="text-emerald-500 text-xl mt-0.5"
            />
            <span>Grammar rules & quizzes</span>
          </li>
          <li class="flex items-start gap-3 text-slate-700">
            <Icon
              name="ph:check-circle-fill"
              class="text-emerald-500 text-xl mt-0.5"
            />
            <span>Limited daily AI conversation (5 mins)</span>
          </li>
        </ul>

        <NuxtLink
          to="/learn/basic"
          class="w-full block text-center py-4 rounded-xl bg-slate-100 text-slate-900 font-bold hover:bg-slate-200 transition"
        >
          Start Basic Training
        </NuxtLink>
      </div>

      <!-- Advanced Plan (Paid) -->
      <div
        class="bg-gradient-to-b from-indigo-900 to-slate-900 rounded-3xl p-8 shadow-2xl hover:scale-[1.02] transition-transform flex flex-col relative border border-indigo-500/30"
      >
        <div class="absolute -top-5 inset-x-0 flex justify-center">
          <span
            class="bg-gradient-to-r from-indigo-500 to-purple-500 text-white text-sm font-bold px-6 py-1.5 rounded-full shadow-lg"
            >RECOMMENDED</span
          >
        </div>
        <div class="mb-8 mt-4">
          <h2 class="text-3xl font-bold mb-2 text-white">Advanced Level</h2>
          <p class="text-indigo-200">
            For serious learners aiming for fluency.
          </p>
          <div class="mt-6 flex items-baseline gap-2">
            <span class="text-5xl font-extrabold text-white">$19</span>
            <span class="text-indigo-300 font-medium">/ month</span>
          </div>
        </div>

        <ul class="space-y-4 mb-8 flex-1">
          <li class="flex items-start gap-3 text-slate-200">
            <Icon
              name="ph:check-circle-fill"
              class="text-indigo-400 text-xl mt-0.5"
            />
            <span>Everything in Basic, plus:</span>
          </li>
          <li class="flex items-start gap-3 text-slate-200">
            <Icon
              name="ph:check-circle-fill"
              class="text-indigo-400 text-xl mt-0.5"
            />
            <span>Unlimited Gemini AI conversation sessions</span>
          </li>
          <li class="flex items-start gap-3 text-slate-200">
            <Icon
              name="ph:check-circle-fill"
              class="text-indigo-400 text-xl mt-0.5"
            />
            <span>Real-time voice pronunciation correction</span>
          </li>
          <li class="flex items-start gap-3 text-slate-200">
            <Icon
              name="ph:check-circle-fill"
              class="text-indigo-400 text-xl mt-0.5"
            />
            <span>Business & Professional scenario roleplay</span>
          </li>
        </ul>

        <NuxtLink
          to="/learn/advance"
          class="w-full block text-center py-4 rounded-xl bg-gradient-to-r from-indigo-500 to-purple-500 text-white font-bold hover:shadow-lg hover:from-indigo-400 hover:to-purple-400 transition"
        >
          Upgrade & Start
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
