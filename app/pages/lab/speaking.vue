<template>
  <div
    class="h-full min-h-[500px] flex flex-col bg-white rounded-3xl border border-slate-200 shadow-sm overflow-hidden relative"
  >
    <div
      class="h-16 border-b border-slate-100 bg-slate-50/50 flex items-center justify-between px-6 shrink-0 z-10"
    >
      <div class="flex items-center gap-3">
        <NuxtLink
          to="/dashboard"
          class="w-8 h-8 flex items-center justify-center rounded-full hover:bg-slate-200 text-slate-500 transition"
        >
          <Icon name="ph:x-bold" />
        </NuxtLink>
        <span class="font-bold text-slate-700"
          >Speaking Lab
          <span class="text-slate-400 font-normal"
            >| Coffee Shop Order</span
          ></span
        >
      </div>
      <div class="flex items-center gap-3">
        <button
          @click="showTranscript = !showTranscript"
          class="flex items-center gap-2 text-sm font-medium px-4 py-2 rounded-xl transition"
          :class="
            showTranscript
              ? 'bg-indigo-100 text-indigo-700'
              : 'bg-slate-100 text-slate-600 hover:bg-slate-200'
          "
        >
          <Icon name="ph:subtitles-fill" class="text-lg" />
          {{ showTranscript ? "Hide Transcript" : "Show Transcript" }}
        </button>
      </div>
    </div>

    <div
      class="flex-1 overflow-hidden relative flex flex-col items-center justify-center p-8 bg-[radial-gradient(ellipse_at_center,_var(--tw-gradient-stops))] from-slate-50 via-white to-white"
    >
      <div class="relative mb-12 mt-8">
        <div
          class="w-32 h-32 rounded-full bg-gradient-to-br from-indigo-400 to-purple-500 p-1 shadow-2xl relative z-10 transition-transform duration-500"
          :class="{ 'scale-110': isAiSpeaking }"
        >
          <div
            class="w-full h-full bg-slate-900 rounded-full flex justify-center items-center overflow-hidden relative"
          >
            <div
              class="absolute inset-0 flex items-center justify-center gap-4"
            >
              <div
                class="w-3 h-3 bg-white rounded-full transition-all duration-200"
                :class="{ 'h-1': isAiSpeaking }"
              ></div>
              <div
                class="w-3 h-3 bg-white rounded-full transition-all duration-200"
                :class="{ 'h-1': isAiSpeaking }"
              ></div>
            </div>
            <div
              class="absolute bottom-8 w-8 h-2 bg-white rounded-full transition-all duration-100"
              :class="{ 'h-6 rounded-3xl': isAiSpeaking }"
            ></div>
          </div>
        </div>

        <div
          v-if="isAiSpeaking"
          class="absolute inset-0 bg-indigo-400 rounded-full animate-ping opacity-30 z-0"
        ></div>
        <div
          v-if="isAiSpeaking"
          class="absolute -inset-4 bg-purple-400 rounded-full animate-pulse opacity-20 z-0"
        ></div>

        <div
          class="absolute -top-16 left-1/2 -translate-x-1/2 w-max max-w-xs bg-amber-50 border border-amber-200 text-amber-800 text-sm p-3 rounded-2xl rounded-bl-sm shadow-lg shadow-amber-100/50 z-20 flex gap-2 animate-bounce"
        >
          <Icon
            name="ph:lightbulb-fill"
            class="text-amber-500 text-lg shrink-0"
          />
          <span
            ><strong class="font-bold">Grammar check:</strong> "I would like a
            coffee" sounds more natural.</span
          >
        </div>
      </div>

      <div
        v-if="showTranscript"
        class="w-full max-w-2xl bg-white/80 backdrop-blur-md border border-slate-200 rounded-2xl p-6 shadow-sm overflow-y-auto mb-8 max-h-[30vh] custom-scrollbar"
      >
        <div class="space-y-4">
          <div class="flex gap-3">
            <div
              class="w-8 h-8 rounded-full bg-indigo-100 flex items-center justify-center text-indigo-600 text-xs font-bold shrink-0"
            >
              AI
            </div>
            <p
              class="text-slate-700 bg-slate-50 p-3 rounded-2xl rounded-tl-none border border-slate-100"
            >
              Welcome to Starbeans. What can I get started for you today?
            </p>
          </div>
          <div class="flex gap-3 flex-row-reverse">
            <div
              class="w-8 h-8 rounded-full bg-emerald-100 flex items-center justify-center text-emerald-600 text-xs font-bold shrink-0"
            >
              YOU
            </div>
            <p
              class="text-slate-800 bg-emerald-50 p-3 rounded-2xl rounded-tr-none border border-emerald-100"
            >
              I am wanting coffee please.
            </p>
          </div>
          <div class="flex gap-3">
            <div
              class="w-8 h-8 rounded-full bg-indigo-100 flex items-center justify-center text-indigo-600 text-xs font-bold shrink-0"
            >
              AI
            </div>
            <p
              class="text-slate-700 bg-slate-50 p-3 rounded-2xl rounded-tl-none border border-slate-100"
            >
              Sure thing. Would you like that hot or iced? And what size?
            </p>
          </div>
        </div>
      </div>
      <div v-else class="text-slate-400 text-sm font-medium italic mb-8">
        Transcript hidden. Focus on listening!
      </div>
    </div>

    <div
      class="h-32 bg-slate-900 border-t border-slate-800 flex items-center justify-center px-8 relative shrink-0"
    >
      <div
        class="absolute inset-0 flex items-center justify-center opacity-30 pointer-events-none gap-1"
      >
        <div
          v-for="i in 40"
          :key="i"
          class="w-1.5 bg-emerald-400 rounded-full transition-all duration-75"
          :style="{
            height: isUserSpeaking ? Math.random() * 40 + 10 + 'px' : '4px',
          }"
        ></div>
      </div>

      <button
        @mousedown="startSpeaking"
        @mouseup="stopSpeaking"
        @mouseleave="stopSpeaking"
        @touchstart="startSpeaking"
        @touchend="stopSpeaking"
        class="w-20 h-20 rounded-full flex items-center justify-center z-10 transition-all duration-200 focus:outline-none"
        :class="
          isUserSpeaking
            ? 'bg-emerald-500 scale-110 shadow-[0_0_40px_rgba(16,185,129,0.5)]'
            : 'bg-white hover:bg-slate-100 shadow-xl'
        "
      >
        <Icon
          name="ph:microphone-fill"
          class="text-4xl"
          :class="isUserSpeaking ? 'text-white' : 'text-slate-800'"
        />
      </button>

      <p class="absolute bottom-3 text-slate-400 text-xs font-medium">
        Hold spacebar or button to speak
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

definePageMeta({
  layout: "workspace",
});

const showTranscript = ref(true);
const isAiSpeaking = ref(false);
const isUserSpeaking = ref(false);
let aiInterval = null;

const startSpeaking = () => {
  isUserSpeaking.value = true;
  isAiSpeaking.value = false;
};

const stopSpeaking = () => {
  if (!isUserSpeaking.value) return;
  isUserSpeaking.value = false;
  setTimeout(() => {
    isAiSpeaking.value = true;
    setTimeout(() => {
      isAiSpeaking.value = false;
    }, 4000);
  }, 1000);
};

onMounted(() => {
  aiInterval = setInterval(() => {
    if (!isUserSpeaking.value && !isAiSpeaking.value && Math.random() > 0.7) {
      isAiSpeaking.value = true;
      setTimeout(() => (isAiSpeaking.value = false), 2000);
    }
  }, 5000);
});

onUnmounted(() => {
  clearInterval(aiInterval);
});
</script>
