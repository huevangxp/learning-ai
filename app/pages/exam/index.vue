<template>
  <div class="min-h-screen flex flex-col pt-8 overflow-hidden relative">
    <div
      v-if="confettiActive"
      class="absolute inset-0 z-50 pointer-events-none flex items-center justify-center"
    >
      <div class="text-center animate-bounce">
        <Icon
          name="ph:party-base-fill"
          class="text-9xl text-amber-400 drop-shadow-[0_0_30px_rgba(251,191,36,0.5)]"
        />
        <h1
          class="text-6xl font-extrabold text-white mt-4 tracking-tight drop-shadow-lg"
        >
          LEVEL UP!
        </h1>
      </div>
    </div>

    <!-- Lockdown Header -->
    <header
      class="max-w-4xl mx-auto w-full flex items-center justify-between bg-slate-800/50 backdrop-blur border border-slate-700 p-4 rounded-2xl shadow-2xl relative z-10"
    >
      <div class="flex items-center gap-3">
        <Icon
          name="ph:shield-check-fill"
          class="text-red-500 text-2xl animate-pulse"
        />
        <div>
          <h2 class="font-bold text-white leading-tight">Exam Lockdown Mode</h2>
          <p class="text-xs text-slate-400">Do not close this application</p>
        </div>
      </div>

      <div
        class="bg-slate-900 border border-slate-700 px-6 py-2 rounded-xl text-center shadow-inner"
      >
        <p
          class="font-mono text-2xl font-black"
          :class="timeLeft < 300 ? 'text-red-400' : 'text-emerald-400'"
        >
          {{ formattedTime }}
        </p>
        <p
          class="text-[10px] text-slate-500 font-bold uppercase tracking-widest mt-0.5"
        >
          Time Remaining
        </p>
      </div>

      <button
        @click="submitExam"
        class="bg-indigo-600 hover:bg-indigo-500 text-white font-bold px-6 py-2.5 rounded-xl shadow-lg hover:shadow-indigo-500/50 transition"
      >
        Submit Final
      </button>
    </header>

    <!-- Main Exam Body -->
    <main
      class="flex-1 max-w-4xl mx-auto w-full my-8 relative z-10 flex flex-col min-h-0"
    >
      <div
        class="bg-slate-800 rounded-3xl border border-slate-700 shadow-2xl overflow-hidden flex flex-col flex-1 relative h-full"
      >
        <div class="h-1.5 w-full bg-slate-700">
          <div
            class="h-full bg-gradient-to-r from-emerald-400 to-indigo-500 w-[95%]"
          ></div>
        </div>

        <div
          class="p-8 border-b border-slate-700 bg-slate-800/80 flex justify-between items-center shrink-0"
        >
          <div>
            <h3
              class="text-sm font-bold text-indigo-400 uppercase tracking-widest mb-1"
            >
              Part 4: The Grand Finale
            </h3>
            <h1 class="text-3xl font-extrabold text-white">
              Live AI Conversation
            </h1>
          </div>
          <div
            class="px-4 py-2 bg-slate-900 rounded-lg border border-slate-700 text-slate-300 text-sm font-medium"
          >
            Wait for the AI to respond, then reply via microphone.
          </div>
        </div>

        <div class="flex-1 flex flex-col p-8 space-y-6 overflow-y-auto">
          <div class="flex gap-4 max-w-[80%]">
            <div
              class="w-12 h-12 rounded-2xl bg-gradient-to-br from-indigo-500 to-purple-500 flex items-center justify-center shrink-0 shadow-lg border border-indigo-400/30"
            >
              <Icon name="ph:robot-fill" class="text-white text-xl" />
            </div>
            <div
              class="bg-slate-700 text-slate-200 p-5 rounded-2xl rounded-tl-sm border border-slate-600 text-[15px] leading-relaxed shadow-md"
            >
              Welcome to the final stage of your exam. Let's pretend we are in a
              job interview. Tell me about a time you overcame a significant
              challenge at work.
            </div>
          </div>

          <div class="flex gap-4 max-w-[80%] self-end flex-row-reverse">
            <div
              class="w-12 h-12 rounded-2xl bg-emerald-500 flex items-center justify-center shrink-0 shadow-lg border border-emerald-400/30"
            >
              <Icon name="ph:user-fill" class="text-white text-xl" />
            </div>
            <div
              class="bg-indigo-600 text-white p-5 rounded-2xl rounded-tr-sm border border-indigo-500 text-[15px] leading-relaxed shadow-md"
            >
              In my last role, we had a major project deadline moved up by two
              weeks. I organized a daily stand-up meeting with my team to
              re-prioritize tasks. Ultimately, we delivered it on time.
            </div>
          </div>

          <div class="flex justify-center my-4">
            <span
              class="bg-slate-900 border border-slate-700 rounded-full px-4 py-2 text-xs font-medium text-slate-400 flex items-center gap-2"
            >
              <Icon name="ph:spinner-gap-bold" class="animate-spin text-sm" />
              Verifying Grammar & Context Matrix...
            </span>
          </div>
        </div>

        <div
          class="p-6 bg-slate-900 border-t border-slate-700 flex justify-center pb-8 shrink-0 relative overflow-hidden"
        >
          <div
            class="absolute inset-0 bg-gradient-to-t from-emerald-500/10 to-transparent"
          ></div>
          <button
            class="w-[300px] h-16 bg-emerald-500 hover:bg-emerald-400 text-white rounded-2xl shadow-[0_0_30px_rgba(16,185,129,0.3)] hover:shadow-[0_0_40px_rgba(16,185,129,0.5)] transition flex items-center justify-center gap-3 font-bold text-lg border border-emerald-400 relative z-10 group cursor-pointer"
          >
            <Icon
              name="ph:microphone-fill"
              class="text-2xl group-hover:scale-110 transition"
            />
            Hold to Respond
          </button>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";

definePageMeta({
  layout: "exam",
});

const totalSeconds = ref(30 * 60);
let timer = null;
const confettiActive = ref(false);

const startTimer = () => {
  timer = setInterval(() => {
    if (totalSeconds.value > 0) {
      totalSeconds.value--;
    } else {
      clearInterval(timer);
      submitExam();
    }
  }, 1000);
};

const formattedTime = computed(() => {
  const m = Math.floor(totalSeconds.value / 60)
    .toString()
    .padStart(2, "0");
  const s = (totalSeconds.value % 60).toString().padStart(2, "0");
  return `${m}:${s}`;
});

const timeLeft = computed(() => totalSeconds.value);

const submitExam = () => {
  confettiActive.value = true;
  clearInterval(timer);
  setTimeout(() => {
    alert("Exam Passed! Moving to B2 Level Dashboard.");
  }, 4000);
};

onMounted(() => {
  startTimer();
});

onUnmounted(() => {
  clearInterval(timer);
});
</script>
