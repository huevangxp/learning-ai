<template>
  <div class="h-full flex flex-col overflow-hidden">
    <!-- Session State: Level Selection -->
    <div
      v-if="!sessionStarted"
      class="flex-1 flex items-center justify-center p-8 overflow-y-auto"
    >
      <div class="max-w-4xl w-full">
        <div class="text-center mb-12 animate-float-up">
          <div
            class="w-20 h-20 bg-indigo-600 rounded-[2rem] flex items-center justify-center mx-auto mb-6 shadow-2xl shadow-indigo-600/20"
          >
            <Icon name="ph:microphone-fill" class="text-white text-4xl" />
          </div>
          <h1 class="text-4xl font-black text-slate-900 tracking-tight mb-3">
            AI Speaking Lab
          </h1>
          <p class="text-slate-500 text-lg font-medium">
            Select your proficiency level to start a personalized practice
            session.
          </p>
        </div>

        <div class="grid md:grid-cols-3 gap-6">
          <button
            v-for="level in levels"
            :key="level.id"
            @click="startSession(level)"
            class="group bg-white border border-slate-200 p-8 rounded-[2.5rem] text-left hover:border-indigo-600 hover:shadow-2xl hover:shadow-indigo-600/10 transition-all duration-500 relative overflow-hidden active:scale-[0.98]"
          >
            <div
              :class="[
                'w-14 h-14 rounded-2xl flex items-center justify-center mb-6 transition-transform group-hover:scale-110 duration-500',
                level.colorClass,
              ]"
            >
              <Icon :name="level.icon" class="text-3xl" />
            </div>
            <h3 class="text-xl font-black text-slate-900 mb-2">
              {{ level.name }}
            </h3>
            <p class="text-sm text-slate-500 font-medium leading-relaxed">
              {{ level.description }}
            </p>

            <div class="mt-6 flex items-center justify-between">
              <span
                class="text-[10px] font-black text-slate-400 uppercase tracking-widest"
                >{{ level.topics }} Topics</span
              >
              <div
                class="w-8 h-8 rounded-full bg-slate-100 flex items-center justify-center text-slate-400 group-hover:bg-indigo-600 group-hover:text-white transition-colors"
              >
                <Icon name="ph:arrow-right-bold" />
              </div>
            </div>

            <!-- Level Indicator Background -->
            <div
              class="absolute -right-4 -top-4 text-8xl font-black text-slate-50 opacity-[0.03] pointer-events-none group-hover:opacity-[0.06] transition-opacity"
            >
              {{ level.id }}
            </div>
          </button>
        </div>
      </div>
    </div>

    <!-- Active Session View -->
    <div
      v-else
      class="flex-1 flex overflow-hidden animate-in fade-in duration-700"
    >
      <!-- Left: Navigation/Levels Column (Minimized) -->
      <div
        class="w-20 border-r border-slate-200/60 flex flex-col items-center py-6 gap-6 bg-white/50 backdrop-blur"
      >
        <div
          v-for="l in levels"
          :key="l.id"
          :class="[
            'w-12 h-12 rounded-2xl flex items-center justify-center transition-all cursor-pointer group relative',
            currentLevel?.id === l.id
              ? 'bg-indigo-600 text-white shadow-lg shadow-indigo-600/30 ring-4 ring-indigo-50'
              : 'bg-white border border-slate-200 text-slate-400 hover:border-indigo-200 hover:text-indigo-600',
          ]"
          @click="currentLevel = l"
        >
          <span class="text-xs font-black">{{ l.id }}</span>
          <!-- Tooltip -->
          <div
            class="absolute left-full ml-4 px-3 py-1.5 bg-slate-900 text-white text-[10px] font-black rounded-lg opacity-0 group-hover:opacity-100 pointer-events-none transition-opacity whitespace-nowrap z-50"
          >
            {{ l.name }}
          </div>
        </div>
        <div class="mt-auto">
          <button
            @click="sessionStarted = false"
            class="w-12 h-12 rounded-2xl bg-rose-50 text-rose-500 flex items-center justify-center hover:bg-rose-500 hover:text-white transition-all shadow-sm"
          >
            <Icon name="ph:x-bold" />
          </button>
        </div>
      </div>

      <!-- Center: Main Chat Area -->
      <div class="flex-1 flex flex-col bg-slate-50/50 relative overflow-hidden">
        <!-- Chat Header -->
        <div
          class="h-20 shrink-0 border-b border-slate-200/60 bg-white/50 backdrop-blur px-8 flex items-center justify-between"
        >
          <div class="flex items-center gap-4">
            <div
              class="w-10 h-10 rounded-2xl bg-indigo-100 text-indigo-600 flex items-center justify-center"
            >
              <Icon name="ph:microphone-stage-bold" class="text-xl" />
            </div>
            <div>
              <h2 class="text-base font-black text-slate-900 tracking-tight">
                {{ currentLevel?.name }} Practice
              </h2>
              <p
                class="text-[10px] font-bold text-slate-400 uppercase tracking-widest"
              >
                Topic: {{ currentTopic }}
              </p>
            </div>
          </div>

          <div class="flex items-center gap-3">
            <div
              class="px-4 py-2 bg-emerald-50 border border-emerald-100 rounded-2xl flex items-center gap-2"
            >
              <div
                class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"
              ></div>
              <span class="text-[10px] font-black text-emerald-700 uppercase"
                >AI Analyst Active</span
              >
            </div>
            <button
              @click="showAnalysis = !showAnalysis"
              class="w-10 h-10 rounded-2xl bg-white border border-slate-200 text-slate-500 flex items-center justify-center hover:bg-slate-50 transition-all"
            >
              <Icon
                :name="showAnalysis ? 'ph:chart-bar-fill' : 'ph:chart-bar-bold'"
                class="text-xl"
              />
            </button>
          </div>
        </div>

        <!-- Chat Container -->
        <div
          ref="chatArea"
          class="flex-1 overflow-y-auto p-10 space-y-8 custom-scrollbar"
        >
          <div
            v-for="(msg, i) in messages"
            :key="i"
            :class="[
              'flex gap-4 group',
              msg.role === 'user' ? 'flex-row-reverse' : '',
            ]"
          >
            <!-- Avatar Hook -->
            <div class="shrink-0 mt-1">
              <div
                v-if="msg.role === 'ai'"
                class="w-11 h-11 rounded-2xl bg-gradient-to-br from-indigo-600 to-purple-700 text-white flex items-center justify-center shadow-lg shadow-indigo-600/20"
              >
                <Icon name="ph:robot-bold" class="text-xl" />
              </div>
              <div
                v-else
                class="w-11 h-11 rounded-2xl bg-slate-900 text-white flex items-center justify-center font-black text-xs shadow-lg shadow-black/10"
              >
                JD
              </div>
            </div>

            <!-- Message Bubble -->
            <div
              :class="[
                'max-w-[70%] space-y-3',
                msg.role === 'user' ? 'text-right' : '',
              ]"
            >
              <div
                :class="[
                  'p-6 rounded-[2rem] text-sm leading-relaxed shadow-sm transition-all duration-300',
                  msg.role === 'ai'
                    ? 'bg-white text-slate-700 border border-slate-200/60 rounded-tl-lg'
                    : 'bg-indigo-600 text-white font-medium rounded-tr-lg shadow-xl shadow-indigo-600/10',
                ]"
              >
                {{ msg.text }}

                <!-- Audio Player Inline (Minimal) -->
                <div
                  v-if="msg.role === 'ai'"
                  class="mt-4 pt-4 border-t border-slate-100 flex items-center gap-3"
                >
                  <button
                    class="w-8 h-8 rounded-xl bg-indigo-50 text-indigo-600 flex items-center justify-center hover:bg-indigo-100 transition-colors"
                  >
                    <Icon name="ph:play-fill" />
                  </button>
                  <div
                    class="flex-1 h-1 bg-slate-100 rounded-full overflow-hidden"
                  >
                    <div class="h-full bg-indigo-200 w-1/3"></div>
                  </div>
                  <span class="text-[10px] font-bold text-slate-400">0:24</span>
                </div>
              </div>

              <!-- Metrics/Feedback Bubbles -->
              <div
                v-if="msg.feedback"
                class="animate-in fade-in slide-in-from-top-2 duration-500"
              >
                <div
                  class="bg-amber-50/80 backdrop-blur border border-amber-200/50 rounded-2xl p-4 flex items-start gap-3"
                >
                  <div
                    class="w-8 h-8 rounded-xl bg-amber-400 text-white flex items-center justify-center shrink-0"
                  >
                    <Icon name="ph:lightbulb-fill" />
                  </div>
                  <div>
                    <p
                      class="text-[10px] font-black text-amber-800 uppercase tracking-widest leading-none mb-1.5"
                    >
                      Improvement Tip
                    </p>
                    <p class="text-sm text-amber-700 leading-relaxed">
                      {{ msg.feedback }}
                    </p>
                  </div>
                </div>
              </div>

              <div
                v-if="msg.score"
                class="flex items-center gap-2 text-[10px] font-black text-emerald-600 uppercase tracking-widest justify-end"
              >
                <Icon name="ph:microphone-fill" />
                Score: {{ msg.score }}% Perfect
              </div>
            </div>
          </div>

          <!-- Typing state -->
          <div v-if="isAiTyping" class="flex gap-4">
            <div
              class="w-11 h-11 rounded-2xl bg-indigo-600 text-white flex items-center justify-center"
            >
              <Icon name="ph:robot-bold" class="text-xl" />
            </div>
            <div
              class="bg-white px-6 py-4 rounded-[1.5rem] rounded-tl-sm border border-slate-200 flex gap-1.5 items-center"
            >
              <div
                class="w-2 h-2 rounded-full bg-indigo-200 animate-bounce"
              ></div>
              <div
                class="w-2 h-2 rounded-full bg-indigo-300 animate-bounce"
                style="animation-delay: 0.15s"
              ></div>
              <div
                class="w-2 h-2 rounded-full bg-indigo-400 animate-bounce"
                style="animation-delay: 0.3s"
              ></div>
            </div>
          </div>
        </div>

        <!-- Input Section -->
        <div
          class="p-10 shrink-0 border-t border-slate-200/60 bg-white/50 backdrop-blur"
        >
          <div class="max-w-4xl mx-auto">
            <!-- Waveform (Animated SVG) -->
            <div
              v-if="isRecording"
              class="h-20 flex items-center justify-center mb-8 gap-1.5"
            >
              <div
                v-for="i in 40"
                :key="i"
                class="w-1.5 bg-gradient-to-t from-indigo-600 to-purple-600 rounded-full transition-all duration-300"
                :style="{
                  height: (isRecording ? Math.random() * 60 + 10 : 8) + 'px',
                  opacity: Math.random() * 0.5 + 0.5,
                }"
              ></div>
            </div>

            <div class="flex items-center gap-6">
              <!-- Mic Button -->
              <button
                @click="toggleRecording"
                :class="[
                  'w-20 h-20 rounded-[2rem] flex items-center justify-center text-3xl transition-all duration-500 shadow-2xl relative group',
                  isRecording
                    ? 'bg-rose-500 text-white shadow-rose-500/30'
                    : 'bg-indigo-600 text-white shadow-indigo-600/30 hover:-translate-y-1',
                ]"
              >
                <Icon
                  :name="isRecording ? 'ph:stop-fill' : 'ph:microphone-fill'"
                />
                <div
                  v-if="isRecording"
                  class="absolute inset-0 rounded-[2rem] border-4 border-rose-400 animate-ping opacity-20"
                ></div>
                <div
                  v-if="!isRecording"
                  class="absolute inset-0 rounded-[2rem] bg-white opacity-0 group-hover:opacity-10 transition-opacity"
                ></div>
              </button>

              <!-- Text Input / Message Context -->
              <div class="flex-1 relative">
                <input
                  v-model="userInput"
                  @keydown.enter="sendMessage"
                  :placeholder="
                    isRecording
                      ? 'I am listening... speak naturally'
                      : 'Ask me anything or type to chat...'
                  "
                  class="w-full bg-white border border-slate-200/60 rounded-3xl py-6 px-8 text-base font-medium placeholder:text-slate-400 text-slate-700 shadow-sm focus:outline-none focus:ring-4 focus:ring-indigo-600/5 focus:border-indigo-600 transition-all pr-16"
                  :disabled="isRecording"
                />
                <button
                  @click="sendMessage"
                  class="absolute right-3 top-3 bottom-3 w-14 rounded-2xl bg-slate-900 text-white flex items-center justify-center hover:bg-black transition-colors active:scale-95"
                >
                  <Icon name="ph:arrow-right-bold" class="text-xl" />
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Right: Real-time Analysis Sidebar -->
      <aside
        v-if="showAnalysis"
        class="w-[400px] border-l border-slate-200/60 bg-white flex flex-col animate-in slide-in-from-right duration-500"
      >
        <div
          class="h-20 shrink-0 border-b border-slate-200/60 px-8 flex items-center justify-between"
        >
          <span
            class="text-xs font-black text-slate-400 uppercase tracking-widest"
            >Real-time Analysis</span
          >
          <button
            @click="showAnalysis = false"
            class="text-slate-400 hover:text-slate-900"
          >
            <Icon name="ph:x-bold" />
          </button>
        </div>

        <div class="flex-1 overflow-y-auto p-8 space-y-10 custom-scrollbar">
          <!-- Performance Radar (Simplified) -->
          <div class="space-y-6">
            <div
              v-for="metric in metrics"
              :key="metric.label"
              class="space-y-2"
            >
              <div class="flex items-center justify-between">
                <span class="text-xs font-bold text-slate-700 capitalize">{{
                  metric.label
                }}</span>
                <span
                  :class="[
                    'text-[10px] font-black px-2 py-0.5 rounded-lg border',
                    metric.colorClass,
                  ]"
                >
                  {{ metric.value }}%
                </span>
              </div>
              <div class="h-2 bg-slate-100 rounded-full overflow-hidden">
                <div
                  class="h-full rounded-full transition-all duration-1000"
                  :class="metric.bgClass"
                  :style="{ width: metric.value + '%' }"
                ></div>
              </div>
            </div>
          </div>

          <!-- Vocabulary Builder -->
          <div class="pt-10 border-t border-slate-100">
            <h4
              class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-6"
            >
              Mastered This Session
            </h4>
            <div class="flex flex-wrap gap-2">
              <div
                v-for="word in usedWords"
                :key="word"
                class="bg-slate-50 border border-slate-200/50 rounded-xl px-4 py-2 text-xs font-bold text-slate-600 hover:bg-indigo-600 hover:text-white transition-all cursor-default"
              >
                {{ word }}
              </div>
            </div>
          </div>

          <!-- Session Insights Card -->
          <div
            class="bg-gradient-to-br from-indigo-600 to-purple-700 rounded-3xl p-6 text-white relative overflow-hidden group"
          >
            <div
              class="absolute -right-4 -bottom-4 w-24 h-24 bg-white/10 rounded-full blur-2xl"
            ></div>
            <div class="relative z-10">
              <p
                class="text-[10px] font-black text-white/70 uppercase tracking-widest mb-4"
              >
                Gemini Insight
              </p>
              <p class="text-sm font-bold leading-relaxed mb-6">
                "You tend to hesitate before using past tenses. Let's practice
                irregular verbs next."
              </p>
              <button
                class="w-full py-3 bg-white/20 backdrop-blur rounded-xl text-xs font-black hover:bg-white/30 transition-all"
              >
                Start Verb Drill
              </button>
            </div>
          </div>
        </div>

        <!-- Session Timer Footer -->
        <div
          class="p-8 border-t border-slate-200/60 bg-slate-50/50 flex items-center justify-between"
        >
          <div>
            <p
              class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-1"
            >
              Session Duration
            </p>
            <p class="text-2xl font-black text-slate-900">{{ sessionTime }}</p>
          </div>
          <div
            class="h-12 w-12 rounded-2xl bg-indigo-600/5 border border-indigo-100 flex items-center justify-center text-indigo-600"
          >
            <Icon name="ph:clock-bold" class="text-2xl" />
          </div>
        </div>
      </aside>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: "learn" });

const sessionStarted = ref(false);
const currentLevel = ref(null);
const currentTopic = ref("Free Conversation");
const showAnalysis = ref(true);
const chatArea = ref(null);
const userInput = ref("");
const isRecording = ref(false);
const isAiTyping = ref(false);

const levels = [
  {
    id: "A1-A2",
    name: "Beginner",
    description:
      "Build confidence with basic everyday core vocabulary and simple greetings.",
    icon: "ph:baby-bold",
    topics: 12,
    colorClass: "bg-emerald-50 text-emerald-600",
  },
  {
    id: "B1-B2",
    name: "Intermediate",
    description:
      "Discuss complex topics, express opinions, and improve grammatical accuracy.",
    icon: "ph:student-bold",
    topics: 24,
    colorClass: "bg-indigo-50 text-indigo-600",
  },
  {
    id: "C1-C2",
    name: "Advanced",
    description:
      "Master native-like nuances, idioms, and high-level professional communication.",
    icon: "ph:medal-bold",
    topics: 18,
    colorClass: "bg-purple-50 text-purple-600",
  },
];

const metrics = ref([
  {
    label: "Fluency",
    value: 82,
    bgClass: "bg-emerald-500",
    colorClass: "bg-emerald-50 text-emerald-700 border-emerald-100",
  },
  {
    label: "Vocabulary",
    value: 65,
    bgClass: "bg-indigo-500",
    colorClass: "bg-indigo-50 text-indigo-700 border-indigo-100",
  },
  {
    label: "Pronunciation",
    value: 91,
    bgClass: "bg-purple-500",
    colorClass: "bg-purple-50 text-purple-700 border-purple-100",
  },
  {
    label: "Grammar",
    value: 74,
    bgClass: "bg-amber-500",
    colorClass: "bg-amber-50 text-amber-700 border-amber-100",
  },
]);

const messages = ref([
  {
    role: "ai",
    text: "Hi John! Welcome to the B1 Intermediate Lab. I've prepared a topic about lifestyle balance. How do you usually spend your weekend to relax?",
  },
  {
    role: "user",
    text: "I usually go to the park with my family. We like to walk and enjoy fresh air. It is important for me.",
    score: 88,
  },
]);

const usedWords = ref([
  "lifestyle",
  "balance",
  "relaxed",
  "neighborhood",
  "outdoor",
  "essential",
  "positive",
  "environment",
]);

const seconds = ref(0);
const sessionTime = computed(() => {
  const m = Math.floor(seconds.value / 60);
  const s = seconds.value % 60;
  return `${m}:${s.toString().padStart(2, "0")}`;
});

let timerInterval = null;

function startSession(level) {
  currentLevel.value = level;
  sessionStarted.value = true;
  seconds.value = 0;
  if (timerInterval) clearInterval(timerInterval);
  timerInterval = setInterval(() => seconds.value++, 1000);
}

function toggleRecording() {
  isRecording.value = !isRecording.value;
  if (!isRecording.value) {
    // Simulate thinking
    isAiTyping.value = true;
    setTimeout(() => {
      messages.value.push({
        role: "user",
        text: "Actually, I think spending time outdoors is better than staying home.",
        score: 94,
      });
      isAiTyping.value = false;
      simulateAiResponse();
    }, 1000);
  }
}

function sendMessage() {
  if (!userInput.value.trim()) return;
  messages.value.push({ role: "user", text: userInput.value });
  userInput.value = "";
  simulateAiResponse();
}

function simulateAiResponse() {
  isAiTyping.value = true;
  setTimeout(() => {
    isAiTyping.value = false;
    messages.value.push({
      role: "ai",
      text: "I completely agree! Nature has a way of resetting our energy levels. Do you have a favorite outdoor spot in your city that you visit frequently?",
      feedback:
        "Great sentence! You can also say 'rejuvenating' instead of 'better' to describe the effect of nature.",
    });
    scrollToBottom();
  }, 1500);
}

function scrollToBottom() {
  nextTick(() => {
    if (chatArea.value) {
      chatArea.value.scrollTo({
        top: chatArea.value.scrollHeight,
        behavior: "smooth",
      });
    }
  });
}

onUnmounted(() => {
  if (timerInterval) clearInterval(timerInterval);
});
</script>

<style scoped>
.custom-scrollbar::-webkit-scrollbar {
  width: 4px;
}
.custom-scrollbar::-webkit-scrollbar-track {
  background: transparent;
}
.custom-scrollbar::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.05);
  border-radius: 10px;
}
.custom-scrollbar:hover::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.1);
}

.fire-glow {
  filter: drop-shadow(0 0 6px rgba(249, 115, 22, 0.4));
}
</style>
