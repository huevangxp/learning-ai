<template>
  <div class="h-full flex flex-col overflow-hidden">
    <!-- State 1: Selection Screen (Level & Mode) -->
    <div
      v-if="!sessionStarted"
      class="flex-1 overflow-y-auto p-10 custom-scrollbar"
    >
      <div class="max-w-5xl mx-auto space-y-12">
        <div class="text-center animate-float-up">
          <div
            class="w-20 h-20 bg-purple-600 rounded-[2rem] flex items-center justify-center mx-auto mb-6 shadow-2xl shadow-purple-600/20"
          >
            <Icon name="ph:book-open-text-fill" class="text-white text-4xl" />
          </div>
          <h1 class="text-4xl font-black text-slate-900 tracking-tight mb-3">
            Literacy Lab
          </h1>
          <p class="text-slate-500 text-lg font-medium">
            Master your pronunciation and reading fluency with AI-guided
            practice.
          </p>
        </div>

        <!-- Level Selector -->
        <div class="grid md:grid-cols-3 gap-6">
          <div
            v-for="l in levels"
            :key="l.id"
            @click="selectedLevel = l"
            :class="[
              'p-8 rounded-[2.5rem] border-2 transition-all cursor-pointer group relative overflow-hidden active:scale-[0.98]',
              selectedLevel?.id === l.id
                ? 'border-purple-600 bg-purple-50/50 shadow-xl shadow-purple-600/5'
                : 'border-slate-200 bg-white hover:border-purple-300',
            ]"
          >
            <div
              :class="[
                'w-12 h-12 rounded-2xl flex items-center justify-center mb-6',
                l.colorClass,
              ]"
            >
              <Icon :name="l.icon" class="text-2xl" />
            </div>
            <h3 class="text-xl font-black text-slate-900 mb-1">{{ l.name }}</h3>
            <p
              class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-4"
            >
              Level {{ l.id }}
            </p>
            <p class="text-sm text-slate-500 font-medium leading-relaxed">
              {{ l.desc }}
            </p>

            <div
              v-if="selectedLevel?.id === l.id"
              class="absolute top-4 right-4 text-purple-600"
            >
              <Icon name="ph:check-circle-fill" class="text-2xl" />
            </div>
          </div>
        </div>

        <!-- Mode Selector -->
        <div class="grid md:grid-cols-3 gap-8 pt-8">
          <button
            v-for="mode in modes"
            :key="mode.id"
            @click="startSession(mode)"
            class="group bg-white border border-slate-200 p-8 rounded-[2.5rem] text-left hover:border-indigo-600 hover:shadow-2xl hover:shadow-indigo-600/10 transition-all duration-500 relative flex flex-col items-start"
            :disabled="!selectedLevel"
          >
            <div
              class="w-14 h-14 rounded-2xl bg-slate-900 text-white flex items-center justify-center mb-6 group-hover:bg-indigo-600 transition-colors"
            >
              <Icon :name="mode.icon" class="text-3xl" />
            </div>
            <h4 class="text-xl font-black text-slate-900 mb-2">
              {{ mode.title }}
            </h4>
            <p class="text-sm text-slate-500 font-medium mb-6 leading-relaxed">
              {{ mode.desc }}
            </p>
            <div class="mt-auto flex items-center justify-between w-full">
              <span
                class="text-[10px] font-black text-purple-600 uppercase tracking-widest"
                >Available Tasks: {{ mode.count }}</span
              >
              <Icon
                name="ph:arrow-circle-right-fill"
                class="text-3xl text-slate-200 group-hover:text-indigo-600 transition-colors"
              />
            </div>
            <div
              v-if="!selectedLevel"
              class="absolute inset-0 bg-white/60 backdrop-blur-[2px] rounded-[2.5rem] flex items-center justify-center"
            >
              <span
                class="px-4 py-1 bg-slate-100 rounded-full text-[10px] font-black text-slate-400 uppercase tracking-widest border border-slate-200"
                >Select Level First</span
              >
            </div>
          </button>
        </div>
      </div>
    </div>

    <!-- State 2: Active Reading Session -->
    <div
      v-else
      class="flex-1 flex overflow-hidden animate-in fade-in duration-700"
    >
      <!-- Left: Navigation/Content Switcher -->
      <div
        class="w-24 border-r border-slate-200/60 bg-white/50 backdrop-blur flex flex-col items-center py-8 gap-6"
      >
        <div
          class="w-14 h-14 rounded-2xl bg-purple-600 text-white flex items-center justify-center shadow-lg shadow-purple-600/20 mb-4"
        >
          <Icon name="ph:book-open-fill" class="text-2xl" />
        </div>
        <div class="flex-1 space-y-4">
          <button
            @click="sessionStarted = false"
            class="w-12 h-12 rounded-2xl bg-white border border-slate-200 text-slate-400 flex items-center justify-center hover:bg-slate-50 hover:text-slate-900 transition-all"
          >
            <Icon name="ph:house-bold" />
          </button>
        </div>
        <button
          @click="sessionStarted = false"
          class="w-12 h-12 rounded-2xl bg-rose-50 text-rose-500 flex items-center justify-center hover:bg-rose-500 hover:text-white transition-all"
        >
          <Icon name="ph:power-bold" />
        </button>
      </div>

      <!-- Center: Reading Material -->
      <div class="flex-1 flex flex-col bg-slate-50/50 relative overflow-hidden">
        <!-- Header -->
        <header
          class="h-20 shrink-0 border-b border-slate-200/60 bg-white/50 backdrop-blur px-10 flex items-center justify-between"
        >
          <div class="flex items-center gap-4">
            <div
              class="px-4 py-1.5 bg-purple-50 border border-purple-100 rounded-full"
            >
              <span
                class="text-[10px] font-black text-purple-600 uppercase tracking-widest"
                >{{ selectedLevel?.id }} Proficiency</span
              >
            </div>
            <h2 class="text-base font-black text-slate-900 tracking-tight">
              {{ currentContent?.title }}
            </h2>
          </div>

          <div class="flex items-center gap-4">
            <div
              class="flex bg-white border border-slate-200 rounded-xl p-1 shadow-sm"
            >
              <button
                @click="fontSize = Math.max(14, fontSize - 2)"
                class="w-8 h-8 rounded-lg hover:bg-slate-50 transition-colors flex items-center justify-center text-slate-400"
              >
                <Icon name="ph:text-t-bold" class="text-sm" />
              </button>
              <div class="w-[1px] h-4 bg-slate-200 self-center mx-1"></div>
              <button
                @click="fontSize = Math.min(24, fontSize + 2)"
                class="w-8 h-8 rounded-lg hover:bg-slate-50 transition-colors flex items-center justify-center text-slate-900"
              >
                <Icon name="ph:text-t-bold" class="text-lg" />
              </button>
            </div>
            <button
              @click="speakContent"
              class="w-10 h-10 rounded-xl bg-purple-100 text-purple-600 flex items-center justify-center hover:bg-purple-600 hover:text-white transition-all"
            >
              <Icon
                :name="
                  isListening ? 'ph:speaker-high-fill' : 'ph:speaker-none-bold'
                "
                class="text-xl"
              />
            </button>
          </div>
        </header>

        <!-- Main Reading Area -->
        <div class="flex-1 overflow-y-auto p-16 custom-scrollbar relative">
          <div class="max-w-3xl mx-auto">
            <!-- Content Display -->
            <div class="animate-in slide-in-from-bottom duration-700">
              <!-- Vocab Mode -->
              <div v-if="selectedMode === 'vocab'" class="space-y-8">
                <div
                  v-for="(item, idx) in currentContent?.items"
                  :key="idx"
                  class="p-8 bg-white border border-slate-200/60 rounded-[2rem] shadow-sm hover:shadow-xl hover:shadow-purple-600/5 transition-all group flex items-center justify-between"
                >
                  <div>
                    <p
                      class="text-3xl font-black text-slate-900 mb-2 leading-tight"
                    >
                      {{ item.word }}
                    </p>
                    <p class="text-sm text-slate-500 font-medium">
                      {{ item.meaning }}
                    </p>
                  </div>
                  <div class="flex gap-2">
                    <button
                      @click="speakWord(item.word)"
                      class="w-12 h-12 rounded-2xl bg-purple-50 text-purple-600 flex items-center justify-center hover:bg-purple-600 hover:text-white transition-all"
                    >
                      <Icon name="ph:speaker-high-bold" class="text-xl" />
                    </button>
                  </div>
                </div>
              </div>

              <!-- Text/Story Mode -->
              <div v-else class="space-y-8">
                <article
                  class="reading-content text-slate-800 leading-[2] font-medium transition-all"
                  :style="{ fontSize: fontSize + 'px' }"
                >
                  <p
                    v-for="(p, i) in currentContent?.paragraphs"
                    :key="i"
                    class="mb-8"
                  >
                    <span
                      v-for="(word, wi) in p.split(' ')"
                      :key="wi"
                      :class="[
                        'inline-block mr-1.5 transition-all duration-300 rounded-md px-1',
                        isMatching(word)
                          ? 'bg-emerald-100 text-emerald-800 font-bold'
                          : '',
                        errorIndices.includes(wi)
                          ? 'bg-rose-100 text-rose-800'
                          : '',
                      ]"
                      >{{ word }}</span
                    >
                  </p>
                </article>
              </div>
            </div>
          </div>
        </div>

        <!-- Footer Control Bar -->
        <div class="p-8 border-t border-slate-200/60 bg-white/50 backdrop-blur">
          <div class="max-w-3xl mx-auto flex items-center gap-8">
            <button
              @click="toggleListening"
              :class="[
                'w-24 h-24 rounded-[2.5rem] flex flex-col items-center justify-center transition-all duration-500 shadow-2xl relative overflow-hidden group',
                isRecording
                  ? 'bg-rose-500 text-white shadow-rose-500/30'
                  : 'bg-indigo-600 text-white shadow-indigo-600/30 hover:-translate-y-1',
              ]"
            >
              <Icon
                :name="isRecording ? 'ph:stop-fill' : 'ph:microphone-fill'"
                class="text-3xl mb-1 z-10"
              />
              <span
                class="text-[10px] font-black uppercase tracking-widest z-10"
                >{{ isRecording ? "STOP" : "READ" }}</span
              >
              <div
                v-if="isRecording"
                class="absolute inset-0 bg-white/10 animate-pulse"
              ></div>
            </button>

            <div class="flex-1 space-y-4">
              <div v-if="isRecording" class="h-12 flex items-center gap-1">
                <div
                  v-for="i in 30"
                  :key="i"
                  class="flex-1 bg-indigo-600/30 rounded-full transition-all duration-100"
                  :style="{ height: Math.random() * 100 + '%' }"
                ></div>
              </div>
              <div
                v-else-if="analysisResult"
                class="animate-in fade-in duration-500"
              >
                <div
                  :class="[
                    'px-6 py-4 rounded-2xl flex items-center gap-4 border',
                    analysisResult.success
                      ? 'bg-emerald-50 border-emerald-100'
                      : 'bg-rose-50 border-rose-100',
                  ]"
                >
                  <div
                    :class="[
                      'w-10 h-10 rounded-xl flex items-center justify-center shrink-0',
                      analysisResult.success
                        ? 'bg-emerald-500 text-white'
                        : 'bg-rose-500 text-white',
                    ]"
                  >
                    <Icon
                      :name="
                        analysisResult.success
                          ? 'ph:sparkle-fill'
                          : 'ph:warning-circle-fill'
                      "
                      class="text-xl"
                    />
                  </div>
                  <div>
                    <p
                      :class="[
                        'text-xs font-black uppercase tracking-widest mb-0.5',
                        analysisResult.success
                          ? 'text-emerald-700'
                          : 'text-rose-700',
                      ]"
                    >
                      {{
                        analysisResult.success
                          ? "AI Analysis Complete"
                          : "AI Error: Listening Failed"
                      }}
                    </p>
                    <p
                      :class="[
                        'text-sm font-bold',
                        analysisResult.success
                          ? 'text-emerald-900'
                          : 'text-rose-900',
                      ]"
                    >
                      {{ analysisResult.message }}
                    </p>
                  </div>
                </div>
              </div>
              <div
                v-else
                class="text-slate-400 font-bold text-sm bg-slate-100/50 p-6 rounded-2xl border border-dashed border-slate-200 flex items-center gap-3"
              >
                <Icon name="ph:info-bold" class="text-xl" />
                Tap the microphone and read the text aloud precisely as shown
                above.
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Right: Progress & Stats -->
      <aside
        v-if="sessionStarted"
        class="w-[400px] border-l border-slate-200/60 bg-white flex flex-col animate-in slide-in-from-right duration-500"
      >
        <div
          class="h-20 shrink-0 border-b border-slate-200/60 px-8 flex items-center justify-between"
        >
          <span
            class="text-xs font-black text-slate-400 uppercase tracking-widest"
            >Performance Stats</span
          >
          <div
            class="w-2.5 h-2.5 rounded-full bg-emerald-500 animate-pulse"
          ></div>
        </div>

        <div class="flex-1 overflow-y-auto p-10 space-y-10 custom-scrollbar">
          <!-- Accuracy Ring -->
          <div class="text-center relative py-4">
            <div class="relative inline-flex items-center justify-center">
              <svg class="w-32 h-32 transform -rotate-90">
                <circle
                  cx="64"
                  cy="64"
                  r="56"
                  stroke="currentColor"
                  stroke-width="8"
                  fill="transparent"
                  class="text-slate-100"
                />
                <circle
                  cx="64"
                  cy="64"
                  r="56"
                  stroke="currentColor"
                  stroke-width="12"
                  fill="transparent"
                  stroke-dasharray="351.8"
                  :stroke-dashoffset="351.8 * (1 - accuracy / 100)"
                  stroke-linecap="round"
                  class="text-purple-600 transition-all duration-1000"
                />
              </svg>
              <div class="absolute flex flex-col">
                <span
                  class="text-3xl font-black text-slate-900 tracking-tighter"
                  >{{ accuracy }}%</span
                >
                <span
                  class="text-[9px] font-black text-slate-400 uppercase tracking-widest"
                  >Accuracy</span
                >
              </div>
            </div>
          </div>

          <!-- Detailed Metrics -->
          <div class="space-y-6">
            <div
              v-for="stat in sessionStats"
              :key="stat.label"
              class="space-y-3"
            >
              <div class="flex justify-between items-center text-xs font-bold">
                <span class="text-slate-500">{{ stat.label }}</span>
                <span class="text-purple-600">{{ stat.value }}%</span>
              </div>
              <div class="h-1.5 bg-slate-100 rounded-full overflow-hidden">
                <div
                  class="h-full bg-purple-600 rounded-full transition-all duration-1000"
                  :style="{ width: stat.value + '%' }"
                ></div>
              </div>
            </div>
          </div>

          <!-- Real-time Transcription Log -->
          <div class="pt-8 border-t border-slate-100">
            <h4
              class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-6"
            >
              Live AI Capture
            </h4>
            <div
              class="bg-slate-50 border border-slate-200 rounded-2xl p-4 min-h-[120px]"
            >
              <p
                v-if="liveTranscript"
                class="text-sm font-medium text-slate-600 leading-relaxed italic animate-pulse"
              >
                "{{ liveTranscript }}..."
              </p>
              <p
                v-else
                class="text-xs text-slate-400 font-medium text-center py-10"
              >
                Start reading to see AI transcription...
              </p>
            </div>
          </div>
        </div>

        <!-- Result Footer -->
        <div class="p-8 border-t border-slate-200/60 bg-slate-50/50">
          <button
            @click="sessionStarted = false"
            class="w-full py-4 bg-slate-900 text-white rounded-2xl text-sm font-black hover:bg-black hover:shadow-xl hover:shadow-black/20 transition-all active:scale-95 flex items-center justify-center gap-2"
          >
            Complete Session <Icon name="ph:check-bold" />
          </button>
        </div>
      </aside>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: "learn" });

const sessionStarted = ref(false);
const selectedLevel = ref(null);
const selectedMode = ref(null);
const fontSize = ref(18);
const accuracy = ref(0);
const isRecording = ref(false);
const isListening = ref(false);
const liveTranscript = ref("");
const analysisResult = ref(null);
const errorIndices = ref([]);

const levels = [
  {
    id: "A1-A2",
    name: "Starter",
    desc: "Simple words and short sentences about daily life.",
    icon: "ph:baby-bold",
    colorClass: "bg-emerald-50 text-emerald-600",
  },
  {
    id: "B1-B2",
    name: "Explorer",
    desc: "Complex texts, news articles, and common idiomatic expressions.",
    icon: "ph:compass-bold",
    colorClass: "bg-indigo-50 text-indigo-600",
  },
  {
    id: "C1-C2",
    name: "Scholar",
    desc: "Academic papers, literature, and sophisticated storytelling.",
    icon: "ph:graduation-cap-bold",
    colorClass: "bg-purple-50 text-purple-600",
  },
];

const modes = [
  {
    id: "vocab",
    title: "Read Vocab",
    icon: "ph:alphabet-bold",
    desc: "Practice individual keywords with pronunciation focus.",
    count: 45,
  },
  {
    id: "text",
    title: "Read Text",
    icon: "ph:article-bold",
    desc: "Read medium-length paragraphs for sentence flow.",
    count: 28,
  },
  {
    id: "story",
    title: "Read Story",
    icon: "ph:books-bold",
    desc: "Engage with immersive narratives and storytelling.",
    count: 12,
  },
];

const sessionStats = ref([
  { label: "Fluency", value: 0 },
  { label: "Speed (WPM)", value: 0 },
  { label: "Pronunciation", value: 0 },
]);

const contentLibrary = {
  "A1-A2": {
    vocab: {
      title: "Daily Objects",
      items: [
        { word: "Breakfast", meaning: "The first meal of the day" },
        { word: "Morning", meaning: "The early part of the day" },
      ],
    },
    text: {
      title: "A Day in London",
      paragraphs: [
        "I live in London. London is a big city. People are friendly here. The weather is cold sometimes.",
      ],
    },
    story: {
      title: "The Red Balloon",
      paragraphs: [
        "Lily found a red balloon. She carried it everywhere. One day, it flew away. Lily was sad but she smiled again soon.",
      ],
    },
  },
  "B1-B2": {
    vocab: {
      title: "Business English",
      items: [
        { word: "Acquisition", meaning: "The act of buying another company" },
        { word: "Strategy", meaning: "A plan of action to achieve a goal" },
      ],
    },
    text: {
      title: "The Future of AI",
      paragraphs: [
        "Artificial Intelligence is transforming industries at an unprecedented rate. Experts believe that human-AI collaboration will be the norm within the next decade.",
      ],
    },
    story: {
      title: "The Starry Night",
      paragraphs: [
        "The village below was silent, unaware of the cosmic dance occurring overhead. Vincent watched as the clouds ebbed and flowed like celestial waves.",
      ],
    },
  },
};

const currentContent = computed(() => {
  if (!selectedLevel || !selectedMode) return null;
  return (
    contentLibrary[selectedLevel.id]?.[selectedMode] ||
    contentLibrary["B1-B2"][selectedMode]
  );
});

// Speech Recognition
let recognition = null;
if (
  process.client &&
  (window.SpeechRecognition || window.webkitSpeechRecognition)
) {
  const SpeechRecognition =
    window.SpeechRecognition || window.webkitSpeechRecognition;
  recognition = new SpeechRecognition();
  recognition.continuous = true;
  recognition.interimResults = true;
  recognition.lang = "en-US";

  recognition.onresult = (event) => {
    const transcript = Array.from(event.results)
      .map((result) => result[0])
      .map((result) => result.transcript)
      .join(" ");
    liveTranscript.value = transcript;
    updateAccuracy();
  };

  recognition.onerror = () => {
    analysisResult.value = {
      success: false,
      message: "Could not capture clear audio. Check microphone permissions.",
    };
    isRecording.value = false;
  };
}

function speakWord(word) {
  if (!process.client) return;
  window.speechSynthesis.cancel();
  const ut = new SpeechSynthesisUtterance(word);
  ut.lang = "en-US";
  window.speechSynthesis.speak(ut);
}

function speakContent() {
  if (!process.client || isListening.value) {
    window.speechSynthesis.cancel();
    isListening.value = false;
    return;
  }
  const text =
    currentContent.value?.paragraphs?.join(" ") ||
    currentContent.value?.items?.map((i) => i.word).join(", ");
  const ut = new SpeechSynthesisUtterance(text);
  ut.onstart = () => (isListening.value = true);
  ut.onend = () => (isListening.value = false);
  window.speechSynthesis.speak(ut);
}

function startSession(mode) {
  selectedMode.value = mode.id;
  sessionStarted.value = true;
  accuracy.value = 0;
  liveTranscript.value = "";
  analysisResult.value = null;
  errorIndices.value = [];
}

function toggleListening() {
  if (isRecording.value) {
    isRecording.value = false;
    recognition?.stop();
    finishAnalysis();
  } else {
    isRecording.value = true;
    liveTranscript.value = "";
    analysisResult.value = null;
    recognition?.start();
  }
}

function isMatching(word) {
  const cleaned = word.toLowerCase().replace(/[.,!?;]/g, "");
  return liveTranscript.value.toLowerCase().includes(cleaned);
}

function updateAccuracy() {
  const targetText = currentContent.value?.paragraphs?.join(" ") || "";
  if (!targetText) return;

  const targetWords = targetText
    .toLowerCase()
    .replace(/[.,!?;]/g, "")
    .split(" ");
  const recognizedCount = targetWords.filter((w) => isMatching(w)).length;
  accuracy.value = Math.round((recognizedCount / targetWords.length) * 100);
}

function finishAnalysis() {
  if (accuracy.value > 80) {
    analysisResult.value = {
      success: true,
      message: "Excellent reading! Your pronunciation is clear and steady.",
    };
    sessionStats.value.forEach(
      (s) => (s.value = Math.round(75 + Math.random() * 20)),
    );
  } else if (accuracy.value > 0) {
    analysisResult.value = {
      success: true,
      message: "Good effort. Some words were missed. Try reading a bit slower.",
    };
    sessionStats.value.forEach(
      (s) => (s.value = Math.round(50 + Math.random() * 25)),
    );
  } else {
    analysisResult.value = {
      success: false,
      message:
        "AI failed to recognize your speech. Please speak closer to the mic.",
    };
  }
}

onUnmounted(() => {
  if (process.client) {
    window.speechSynthesis.cancel();
    recognition?.stop();
  }
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

.reading-content span {
  cursor: default;
}
</style>
