<template>
  <div class="h-[calc(100vh-64px)] flex flex-col overflow-hidden">
    <!-- Session Header -->
    <div
      class="shrink-0 flex items-center justify-between px-6 py-3 bg-white border-b border-slate-200"
    >
      <div class="flex items-center gap-4">
        <h2 class="text-lg font-extrabold text-slate-900">AI Speaking Lab</h2>
        <span
          class="bg-indigo-100 text-indigo-700 text-xs font-bold px-3 py-1 rounded-full border border-indigo-200"
          >Session #14</span
        >
        <span
          class="bg-emerald-100 text-emerald-700 text-xs font-bold px-3 py-1 rounded-full border border-emerald-200 flex items-center gap-1"
        >
          <span
            class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"
          ></span>
          Live
        </span>
      </div>
      <div class="flex items-center gap-3">
        <button
          @click="showTranscript = !showTranscript"
          :class="[
            'px-4 py-2 rounded-xl text-sm font-semibold transition-all border flex items-center gap-2',
            showTranscript
              ? 'bg-indigo-50 text-indigo-700 border-indigo-200'
              : 'bg-slate-100 text-slate-600 border-slate-200 hover:bg-slate-200',
          ]"
        >
          <Icon name="ph:subtitles" class="text-lg" />
          {{ showTranscript ? "Hide" : "Show" }} Transcript
        </button>
        <button
          class="px-4 py-2 rounded-xl text-sm font-semibold bg-red-50 text-red-600 border border-red-200 hover:bg-red-100 transition flex items-center gap-2"
        >
          <Icon name="ph:stop-fill" class="text-lg" /> End Session
        </button>
      </div>
    </div>

    <!-- Main Content Area -->
    <div class="flex-1 flex overflow-hidden">
      <!-- Left: Conversation Area -->
      <div class="flex-1 flex flex-col bg-slate-50">
        <!-- Chat Messages -->
        <div
          ref="chatArea"
          class="flex-1 overflow-y-auto p-6 space-y-5 custom-scrollbar"
        >
          <div
            v-for="(msg, i) in messages"
            :key="i"
            :class="[
              'flex gap-3 animate-float-up',
              msg.role === 'user' ? 'justify-end' : '',
            ]"
            :style="{ animationDelay: `${i * 0.1}s` }"
          >
            <!-- AI Message -->
            <template v-if="msg.role === 'ai'">
              <div
                class="w-10 h-10 rounded-2xl bg-white shadow-sm border border-slate-200 flex items-center justify-center text-indigo-600 shrink-0"
              >
                <Icon name="ph:robot-fill" class="text-xl" />
              </div>
              <div class="max-w-[70%]">
                <div
                  class="bg-white rounded-3xl rounded-tl-sm p-5 shadow-sm border border-slate-200 text-sm text-slate-700 leading-relaxed"
                >
                  {{ msg.text }}
                </div>
                <!-- Feedback Bubble (Correction) -->
                <div
                  v-if="msg.feedback"
                  class="mt-2 bg-amber-50 border border-amber-200 rounded-2xl px-4 py-3 text-sm animate-float-up"
                >
                  <div class="flex items-start gap-2">
                    <Icon
                      name="ph:lightbulb-fill"
                      class="text-amber-500 text-lg mt-0.5 shrink-0"
                    />
                    <div>
                      <p
                        class="font-bold text-amber-800 text-xs uppercase tracking-wider mb-1"
                      >
                        Grammar Tip
                      </p>
                      <p class="text-amber-700 text-[13px] leading-relaxed">
                        {{ msg.feedback }}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
            </template>

            <!-- User Message -->
            <template v-else>
              <div class="max-w-[70%]">
                <div
                  class="bg-gradient-to-br from-indigo-600 to-purple-600 text-white rounded-3xl rounded-tr-sm p-5 shadow-md text-sm leading-relaxed"
                >
                  {{ msg.text }}
                </div>
                <p
                  v-if="msg.score"
                  class="text-right mt-1.5 text-xs flex items-center justify-end gap-1"
                >
                  <Icon name="ph:microphone-fill" class="text-emerald-500" />
                  <span class="font-bold text-emerald-600"
                    >Pronunciation: {{ msg.score }}%</span
                  >
                </p>
              </div>
              <div
                class="w-10 h-10 rounded-2xl bg-slate-200 border border-slate-300 flex items-center justify-center text-slate-600 text-xs font-bold shrink-0"
              >
                YOU
              </div>
            </template>
          </div>

          <!-- AI Typing Indicator -->
          <div v-if="isAiTyping" class="flex gap-3 animate-float-up">
            <div
              class="w-10 h-10 rounded-2xl bg-white shadow-sm border border-slate-200 flex items-center justify-center text-indigo-600 shrink-0"
            >
              <Icon name="ph:robot-fill" class="text-xl" />
            </div>
            <div
              class="bg-white rounded-3xl rounded-tl-sm px-5 py-4 shadow-sm border border-slate-200 flex items-center gap-1.5"
            >
              <span
                class="w-2 h-2 rounded-full bg-indigo-400 animate-bounce"
                style="animation-delay: 0s"
              ></span>
              <span
                class="w-2 h-2 rounded-full bg-indigo-400 animate-bounce"
                style="animation-delay: 0.15s"
              ></span>
              <span
                class="w-2 h-2 rounded-full bg-indigo-400 animate-bounce"
                style="animation-delay: 0.3s"
              ></span>
            </div>
          </div>
        </div>

        <!-- Waveform + Input Area -->
        <div class="shrink-0 border-t border-slate-200 bg-white p-6">
          <!-- Waveform Visualization -->
          <div
            v-if="isRecording"
            class="flex items-center justify-center gap-1 mb-4 h-16"
          >
            <div
              v-for="i in 32"
              :key="i"
              class="waveform-bar w-1.5 bg-gradient-to-t from-indigo-500 to-purple-500 rounded-full"
              :style="{
                '--wave-h': `${Math.random() * 40 + 10}px`,
                '--wave-dur': `${Math.random() * 0.5 + 0.4}s`,
                '--wave-delay': `${Math.random() * 0.5}s`,
                height: '8px',
              }"
            ></div>
          </div>

          <!-- Control Bar -->
          <div class="flex items-center gap-4">
            <!-- Mic Button -->
            <button
              @click="toggleRecording"
              :class="[
                'relative w-14 h-14 rounded-full flex items-center justify-center text-2xl transition-all shadow-lg',
                isRecording
                  ? 'bg-red-500 text-white buddy-pulse shadow-red-500/30'
                  : 'bg-gradient-to-br from-indigo-500 to-purple-600 text-white hover:shadow-indigo-500/30 hover:scale-105',
              ]"
            >
              <Icon
                :name="isRecording ? 'ph:stop-fill' : 'ph:microphone-fill'"
              />
              <span
                v-if="isRecording"
                class="absolute -top-1 -right-1 w-4 h-4 bg-red-400 rounded-full animate-ping"
              ></span>
            </button>

            <!-- Text Input -->
            <div class="flex-1 relative">
              <input
                v-model="userInput"
                @keydown.enter="sendMessage"
                type="text"
                :placeholder="
                  isRecording
                    ? 'Recording... speak naturally'
                    : 'Type or tap the mic to speak...'
                "
                :disabled="isRecording"
                class="w-full bg-slate-50 border-2 border-slate-200 rounded-2xl py-4 pl-5 pr-14 text-sm text-slate-700 placeholder-slate-400 focus:outline-none focus:border-indigo-500 focus:bg-white transition-all shadow-inner disabled:opacity-50"
              />
              <button
                @click="sendMessage"
                class="absolute right-2 top-2 bottom-2 w-10 bg-indigo-500 hover:bg-indigo-600 text-white rounded-xl flex items-center justify-center transition"
              >
                <Icon name="ph:paper-plane-right-fill" class="text-lg" />
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Right: AI Buddy + Session Metrics -->
      <div
        class="w-[360px] border-l border-slate-200 bg-white flex flex-col overflow-y-auto custom-scrollbar"
      >
        <!-- AI Buddy Avatar -->
        <div class="p-8 text-center border-b border-slate-100">
          <div
            :class="[
              'mx-auto w-28 h-28 rounded-full bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center text-white shadow-2xl shadow-indigo-500/30 relative',
              isRecording ? 'buddy-pulse' : '',
            ]"
          >
            <Icon name="ph:robot-fill" class="text-5xl" />
            <span
              :class="[
                'absolute bottom-1 right-1 w-5 h-5 rounded-full border-[3px] border-white',
                isRecording ? 'bg-red-500' : 'bg-emerald-500',
              ]"
            ></span>
          </div>
          <h3 class="text-lg font-extrabold text-slate-900 mt-4">
            Gemini Tutor
          </h3>
          <p
            class="text-sm text-slate-500 mt-1 flex items-center justify-center gap-1.5"
          >
            <span class="relative flex h-2 w-2">
              <span
                class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"
              ></span>
              <span
                class="relative inline-flex rounded-full h-2 w-2 bg-emerald-500"
              ></span>
            </span>
            {{ isRecording ? "Listening to you..." : "Ready to practice" }}
          </p>
        </div>

        <!-- Live Session Metrics -->
        <div class="p-6 space-y-6 flex-1">
          <h4
            class="text-xs font-bold text-slate-400 uppercase tracking-widest"
          >
            Live Session Analysis
          </h4>

          <!-- Fluency -->
          <div>
            <div class="flex justify-between items-center mb-2">
              <span class="text-sm font-semibold text-slate-700">Fluency</span>
              <span
                class="text-xs font-bold bg-emerald-100 text-emerald-700 px-2 py-0.5 rounded-full"
                >88%</span
              >
            </div>
            <div class="h-2 bg-slate-100 rounded-full overflow-hidden">
              <div
                class="h-full bg-emerald-500 rounded-full transition-all duration-1000"
                style="width: 88%"
              ></div>
            </div>
          </div>

          <!-- Pronunciation -->
          <div>
            <div class="flex justify-between items-center mb-2">
              <span class="text-sm font-semibold text-slate-700"
                >Pronunciation</span
              >
              <span
                class="text-xs font-bold bg-indigo-100 text-indigo-700 px-2 py-0.5 rounded-full"
                >91%</span
              >
            </div>
            <div class="h-2 bg-slate-100 rounded-full overflow-hidden">
              <div
                class="h-full bg-indigo-500 rounded-full transition-all duration-1000"
                style="width: 91%"
              ></div>
            </div>
          </div>

          <!-- Grammar Accuracy -->
          <div>
            <div class="flex justify-between items-center mb-2">
              <span class="text-sm font-semibold text-slate-700"
                >Grammar Accuracy</span
              >
              <span
                class="text-xs font-bold bg-amber-100 text-amber-700 px-2 py-0.5 rounded-full"
                >74%</span
              >
            </div>
            <div class="h-2 bg-slate-100 rounded-full overflow-hidden">
              <div
                class="h-full bg-amber-500 rounded-full transition-all duration-1000"
                style="width: 74%"
              ></div>
            </div>
          </div>

          <!-- Vocabulary Level -->
          <div>
            <div class="flex justify-between items-center mb-2">
              <span class="text-sm font-semibold text-slate-700"
                >Vocabulary Range</span
              >
              <span
                class="text-xs font-bold bg-purple-100 text-purple-700 px-2 py-0.5 rounded-full"
                >B1+</span
              >
            </div>
            <div class="h-2 bg-slate-100 rounded-full overflow-hidden">
              <div
                class="h-full bg-purple-500 rounded-full transition-all duration-1000"
                style="width: 65%"
              ></div>
            </div>
          </div>

          <!-- Words Used This Session -->
          <div class="bg-slate-50 rounded-2xl p-4 border border-slate-100">
            <p
              class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-3"
            >
              Words Used
            </p>
            <div class="flex flex-wrap gap-1.5">
              <span
                v-for="word in usedWords"
                :key="word"
                class="bg-white text-slate-600 text-[11px] font-medium px-2.5 py-1 rounded-lg border border-slate-200"
              >
                {{ word }}
              </span>
            </div>
          </div>

          <!-- Session Timer -->
          <div
            class="bg-indigo-50 rounded-2xl p-4 border border-indigo-100 flex items-center gap-4"
          >
            <div
              class="w-12 h-12 rounded-xl bg-indigo-100 flex items-center justify-center text-indigo-600 border border-indigo-200"
            >
              <Icon name="ph:timer-fill" class="text-2xl" />
            </div>
            <div>
              <p
                class="text-xs font-bold text-indigo-500 uppercase tracking-widest"
              >
                Session Time
              </p>
              <p class="text-2xl font-extrabold text-indigo-900">
                {{ sessionTime }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: "learn" });

const chatArea = ref(null);
const userInput = ref("");
const isRecording = ref(false);
const isAiTyping = ref(false);
const showTranscript = ref(true);

const messages = ref([
  {
    role: "ai",
    text: "Hi there! Welcome to your speaking session. Today, let's talk about your hobbies. What do you enjoy doing in your free time?",
  },
  {
    role: "user",
    text: "I like to play football with my friends on weekends. It's very fun and help me stay healthy.",
    score: 87,
  },
  {
    role: "ai",
    text: "That sounds great! Playing football is an excellent way to stay active. Can you tell me about a memorable match you played recently?",
    feedback:
      "Good try! Instead of 'help me stay healthy', say 'helps me stay healthy' — remember to add -s for third person singular (it helps).",
  },
  {
    role: "user",
    text: "Yes, last Saturday we played against a team from another neighborhood. We won 3-2 and I scored the winning goal!",
    score: 92,
  },
  {
    role: "ai",
    text: "Wow, you scored the winning goal? That must have been an amazing feeling! How did your teammates react when you scored?",
  },
]);

const usedWords = ref([
  "football",
  "neighborhood",
  "teammates",
  "winning",
  "scored",
  "memorable",
  "healthy",
  "weekends",
  "active",
  "recently",
]);

// Session Timer
const seconds = ref(423);
const sessionTime = computed(() => {
  const m = Math.floor(seconds.value / 60);
  const s = seconds.value % 60;
  return `${m}:${s.toString().padStart(2, "0")}`;
});

let timerInterval = null;
onMounted(() => {
  timerInterval = setInterval(() => seconds.value++, 1000);
});
onUnmounted(() => {
  if (timerInterval) clearInterval(timerInterval);
});

function toggleRecording() {
  isRecording.value = !isRecording.value;
  if (!isRecording.value) {
    // Simulate speech-to-text result
    setTimeout(() => {
      messages.value.push({
        role: "user",
        text: "I think football teaches me about teamwork and discipline.",
        score: 89,
      });
      simulateAiResponse();
    }, 500);
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
      text: "That's a wonderful insight! Teamwork is indeed one of the most valuable lessons from sports. Do you think these skills have helped you in other areas of your life, like school or work?",
      feedback: null,
    });
    nextTick(() => {
      if (chatArea.value)
        chatArea.value.scrollTop = chatArea.value.scrollHeight;
    });
  }, 2000);
}
</script>
