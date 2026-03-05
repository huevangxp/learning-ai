<template>
  <div
    class="h-full min-h-[500px] flex bg-white rounded-3xl border border-slate-200 shadow-sm overflow-hidden"
  >
    <div
      class="w-1/2 border-r border-slate-200 flex flex-col bg-[#fdfaf6] relative"
    >
      <div
        class="p-4 border-b border-slate-200 bg-white/50 backdrop-blur shrink-0 flex items-center justify-between"
      >
        <div class="flex items-center gap-2 text-slate-500">
          <NuxtLink to="/dashboard" class="hover:text-slate-800 transition"
            ><Icon name="ph:arrow-left-bold"
          /></NuxtLink>
          <span class="text-sm font-bold tracking-widest uppercase"
            >Reading Task 04</span
          >
        </div>
        <div class="flex gap-2">
          <button
            class="w-8 h-8 rounded-lg bg-white border border-slate-200 flex items-center justify-center text-slate-600 shadow-sm hover:bg-slate-50"
          >
            <Icon name="ph:text-a-underline-fill" />
          </button>
          <button
            class="w-8 h-8 rounded-lg bg-white border border-slate-200 flex items-center justify-center text-slate-600 shadow-sm hover:bg-slate-50"
          >
            <Icon name="ph:speaker-high-fill" />
          </button>
        </div>
      </div>

      <div
        class="flex-1 overflow-y-auto p-10 custom-scrollbar font-serif text-lg leading-relaxed text-slate-800"
        @mouseup="handleSelection"
      >
        <h2 class="text-3xl font-extrabold font-sans mb-6 text-slate-900">
          The Modern Workplace
        </h2>
        <p class="mb-4">
          In recent years, the concept of the traditional office has undergone a
          <span class="bg-amber-100 rounded px-1 cursor-pointer"
            >paradigm shift</span
          >. With the advent of advanced telecommunication technologies, remote
          work has become an increasingly viable option for many professionals.
        </p>
        <p class="mb-4">
          However, this transition is not without its challenges. Companies must
          now navigate the complexities of asynchronous communication and find
          innovative ways to foster a sense of belonging among distributed
          teams.
        </p>
        <p>
          Managers bear the brunt of this responsibility. They are tasked with
          ensuring productivity without resorting to micromanagement, a delicate
          balance that requires high levels of emotional intelligence and trust.
        </p>

        <div
          v-if="showContextMenu"
          class="absolute z-50 bg-slate-900 text-white rounded-xl shadow-2xl overflow-hidden flex flex-col w-48 text-sm border border-slate-700"
          :style="{
            top: contextMenuPosition.y + 'px',
            left: contextMenuPosition.x + 'px',
          }"
        >
          <div
            class="px-3 py-2 border-b border-slate-700 bg-slate-800 font-sans text-xs text-slate-300 font-bold uppercase tracking-wider"
          >
            AI Assistant
          </div>
          <button
            @click="showContextMenu = false"
            class="px-4 py-2.5 text-left hover:bg-indigo-600 transition flex items-center gap-2 font-sans"
          >
            <Icon name="ph:book-bookmark-fill" class="text-indigo-400" /> Define
          </button>
          <button
            @click="showContextMenu = false"
            class="px-4 py-2.5 text-left hover:bg-indigo-600 transition flex items-center gap-2 font-sans"
          >
            <Icon name="ph:translate-fill" class="text-emerald-400" /> Translate
          </button>
          <button
            @click="showContextMenu = false"
            class="px-4 py-2.5 text-left hover:bg-indigo-600 transition flex items-center gap-2 font-sans"
          >
            <Icon name="ph:chat-teardrop-text-fill" class="text-amber-400" />
            Use in Sentence
          </button>
        </div>
      </div>
    </div>

    <div class="w-1/2 flex flex-col bg-white">
      <div class="p-6 border-b border-slate-100 flex-1 overflow-y-auto">
        <div class="mb-6">
          <h3 class="font-bold text-xl text-slate-900 mb-2">
            Comprehension Check
          </h3>
          <p class="text-slate-500 text-sm">
            Read the passage on the left and answer the questions below.
          </p>
        </div>

        <div class="space-y-6">
          <div class="bg-indigo-50 border border-indigo-100 p-5 rounded-2xl">
            <p class="font-bold text-slate-800 mb-3">
              1. What does "paradigm shift" refer to in the first paragraph?
            </p>
            <textarea
              class="w-full bg-white border border-slate-200 rounded-xl p-3 text-slate-700 focus:outline-none focus:border-indigo-500 shadow-inner min-h-[100px] resize-none"
              placeholder="Type your answer here..."
            ></textarea>
            <div class="flex justify-end mt-3">
              <button
                class="bg-indigo-600 text-white px-4 py-2 rounded-lg text-sm font-bold shadow-md hover:bg-indigo-700 transition flex items-center gap-2"
              >
                Check Answer <Icon name="ph:sparkle-fill" />
              </button>
            </div>
          </div>

          <div class="flex gap-4">
            <div
              class="w-10 h-10 rounded-full bg-gradient-to-tr from-indigo-500 to-purple-500 flex items-center justify-center text-white shrink-0 shadow-md"
            >
              <Icon name="ph:robot-fill" class="text-lg" />
            </div>
            <div
              class="bg-slate-100 rounded-2xl p-4 text-slate-700 text-sm border border-slate-200 relative mt-1"
            >
              <div
                class="absolute w-3 h-3 bg-slate-100 border-l border-t border-slate-200 -left-1.5 top-4 -rotate-45"
              ></div>
              <p>
                I'm waiting for your answer to Question 1! Remember to use your
                own words based on the context of the sentence.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

definePageMeta({
  layout: "workspace",
});

const showContextMenu = ref(false);
const contextMenuPosition = ref({ x: 0, y: 0 });

const handleSelection = (event) => {
  const selection = window.getSelection();
  if (selection && selection.toString().trim().length > 0) {
    const range = selection.getRangeAt(0);
    const rect = range.getBoundingClientRect();

    contextMenuPosition.value = {
      x: rect.left,
      y: rect.bottom + 10,
    };
    showContextMenu.value = true;
  } else {
    showContextMenu.value = false;
  }
};
</script>
