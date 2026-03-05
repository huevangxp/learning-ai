<template>
  <div class="min-h-screen bg-gray-50 flex font-sans">
    <AdminSidebar />
    <div class="flex-1 flex flex-col">
      <header
        class="h-16 bg-white border-b flex items-center justify-between px-6 z-10 sticky top-0 shadow-sm"
      >
        <h1 class="text-xl font-bold text-gray-800">Admin Control Panel</h1>
        <div class="flex items-center gap-6">
          <NuxtLink
            to="/"
            class="text-sm font-medium text-indigo-600 hover:underline flex items-center gap-1"
          >
            <Icon name="ph:arrow-left" /> Back to App
          </NuxtLink>
          <div
            class="w-10 h-10 rounded-full bg-gradient-to-tr from-indigo-500 to-purple-500 text-white flex items-center justify-center font-bold shadow-md cursor-pointer hover:scale-105 transition"
          >
            AD
          </div>
        </div>
      </header>
      <main class="flex-1 p-8 overflow-auto">
        <slot />
      </main>
    </div>
  </div>
</template>
