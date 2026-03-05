<template>
  <div class="min-h-screen bg-slate-50 font-sans text-slate-900">
    <Navbar />
    <main class="pt-16 min-h-[calc(100vh-80px)]">
      <slot />
    </main>
    <footer
      class="bg-white border-t py-6 text-center text-gray-500 text-sm mt-12 block"
    >
      © {{ new Date().getFullYear() }} AIEnglish platform inspired by Gemini.
      Next-gen language learning.
    </footer>
  </div>
</template>
