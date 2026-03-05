<template>
  <nav
    class="fixed top-0 w-full z-50 bg-white/80 backdrop-blur-md border-b border-gray-100 shadow-sm navbar-hide"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">
        <NuxtLink to="/" class="flex items-center gap-2">
          <Icon name="ph:sparkle-fill" class="text-indigo-600 text-2xl" />
          <span
            class="font-bold text-xl bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-purple-600"
          >
            AIEnglish
          </span>
        </NuxtLink>
        <div class="hidden md:flex space-x-8 items-center">
          <NuxtLink
            to="/"
            class="text-gray-600 hover:text-indigo-600 transition font-medium"
            >Home</NuxtLink
          >
          <NuxtLink
            to="/learn"
            class="text-gray-600 hover:text-indigo-600 transition font-medium"
            >Learn Hub</NuxtLink
          >
        </div>
        <div class="flex flex-row items-center space-x-3">
          <NuxtLink
            to="/auth/login"
            class="px-5 py-2.5 rounded-full border-2 border-slate-200 text-slate-700 font-medium hover:bg-slate-50 hover:border-slate-300 transition-all duration-200 text-sm"
          >
            Sign In
          </NuxtLink>
          <NuxtLink
            to="/auth/register"
            class="px-5 py-2.5 rounded-full bg-gradient-to-r from-indigo-600 to-purple-600 text-white font-medium hover:shadow-lg hover:-translate-y-0.5 transition-all duration-200 text-sm shadow-md"
          >
            Get Started Free
          </NuxtLink>
        </div>
      </div>
    </div>
  </nav>
</template>
