<template>
  <nav
    class="fixed top-0 w-full z-50 bg-white/80 backdrop-blur-md border-b border-gray-100 shadow-sm"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">
        <div class="flex items-center gap-2">
          <Icon name="ph:sparkle-fill" class="text-indigo-600 text-2xl" />
          <span
            class="font-bold text-xl bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-purple-600"
          >
            AIEnglish
          </span>
        </div>
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
          <NuxtLink
            to="/admin"
            class="text-gray-600 hover:text-indigo-600 transition flex items-center gap-1 font-medium"
          >
            <Icon name="ph:shield-star" /> Admin
          </NuxtLink>
        </div>
        <div class="flex flex-row items-center space-x-4">
          <NuxtLink
            to="/learn"
            class="px-5 py-2.5 rounded-full bg-gradient-to-r from-indigo-600 to-purple-600 text-white font-medium hover:shadow-lg hover:-translate-y-0.5 transition-all duration-200"
          >
            Start Learning
          </NuxtLink>
        </div>
      </div>
    </div>
  </nav>
</template>
