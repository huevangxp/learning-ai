<template>
  <aside
    class="w-64 bg-slate-900 min-h-screen text-slate-300 flex flex-col border-r border-slate-800 sticky top-0 h-screen"
  >
    <div class="h-16 flex items-center px-6 border-b border-slate-800">
      <Icon name="ph:sparkle-fill" class="text-indigo-400 text-xl mr-2" />
      <span class="text-lg font-bold text-white tracking-wide"
        >AIEnglish Admin</span
      >
    </div>
    <nav class="flex-1 p-4 space-y-2">
      <NuxtLink
        to="/admin"
        class="flex items-center gap-3 px-4 py-3 rounded-lg hover:bg-slate-800 hover:text-white transition"
        active-class="bg-indigo-600/20 text-indigo-400 border border-indigo-500/30"
        exact
      >
        <Icon name="ph:squares-four" /> Dashboard
      </NuxtLink>
      <NuxtLink
        to="/admin/courses"
        class="flex items-center gap-3 px-4 py-3 rounded-lg hover:bg-slate-800 hover:text-white transition"
        active-class="bg-indigo-600/20 text-indigo-400 border border-indigo-500/30"
      >
        <Icon name="ph:book-bookmark" /> Manage Courses
      </NuxtLink>
      <NuxtLink
        to="/admin/users"
        class="flex items-center gap-3 px-4 py-3 rounded-lg hover:bg-slate-800 hover:text-white transition"
        active-class="bg-indigo-600/20 text-indigo-400 border border-indigo-500/30"
      >
        <Icon name="ph:users" /> Users & Billings
      </NuxtLink>
    </nav>
  </aside>
</template>
