<template>
  <!-- Lockdown: No layout chrome -->
  <div
    class="min-h-screen bg-slate-50 flex flex-col"
    :class="{ 'lockdown-mode': examStarted && !examFinished }"
  >
    <!-- Pre-Exam Screen -->
    <div
      v-if="!examStarted && !examFinished"
      class="flex-1 flex items-center justify-center"
    >
      <div class="max-w-lg text-center px-6">
        <div
          class="w-24 h-24 rounded-3xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center mx-auto shadow-2xl shadow-indigo-500/30 mb-8"
        >
          <Icon name="ph:exam-fill" class="text-white text-5xl" />
        </div>
        <h1 class="text-4xl font-extrabold text-slate-900 tracking-tight mb-3">
          B1 → B2 Level-Up Exam
        </h1>
        <p class="text-slate-500 text-lg mb-4">
          Prove your Intermediate mastery to advance
        </p>

        <div
          class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm mb-8 text-left space-y-4"
        >
          <div class="flex items-center gap-4">
            <div
              class="w-10 h-10 rounded-xl bg-indigo-100 text-indigo-600 flex items-center justify-center border border-indigo-200"
            >
              <Icon name="ph:timer" class="text-xl" />
            </div>
            <div>
              <p class="text-sm font-bold text-slate-800">30 Minutes Total</p>
              <p class="text-xs text-slate-500">Timed — no breaks allowed</p>
            </div>
          </div>
          <div class="flex items-center gap-4">
            <div
              class="w-10 h-10 rounded-xl bg-purple-100 text-purple-600 flex items-center justify-center border border-purple-200"
            >
              <Icon name="ph:list-numbers" class="text-xl" />
            </div>
            <div>
              <p class="text-sm font-bold text-slate-800">4 Sections</p>
              <p class="text-xs text-slate-500">
                Grammar, Reading, Writing, and AI Speaking
              </p>
            </div>
          </div>
          <div class="flex items-center gap-4">
            <div
              class="w-10 h-10 rounded-xl bg-amber-100 text-amber-600 flex items-center justify-center border border-amber-200"
            >
              <Icon name="ph:lock-simple" class="text-xl" />
            </div>
            <div>
              <p class="text-sm font-bold text-slate-800">Lockdown Mode</p>
              <p class="text-xs text-slate-500">
                Navigation will be hidden so you can focus
              </p>
            </div>
          </div>
        </div>

        <button
          @click="startExam"
          class="px-10 py-4 rounded-2xl bg-gradient-to-r from-indigo-500 to-purple-600 text-white font-bold text-lg hover:shadow-2xl hover:shadow-indigo-500/30 hover:-translate-y-1 transition-all glow-button"
        >
          Begin Exam
        </button>
        <p class="text-xs text-slate-400 mt-4">
          You need 70% to pass and advance to B2
        </p>
      </div>
    </div>

    <!-- Active Exam -->
    <template v-if="examStarted && !examFinished">
      <!-- Locked Header -->
      <header
        :class="[
          'sticky top-0 z-50 h-16 bg-white border-b border-slate-200 flex items-center justify-between px-8 shadow-sm',
          timeRemaining <= 120 ? 'timer-critical' : '',
        ]"
      >
        <div class="flex items-center gap-4">
          <div
            class="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center text-white shadow-md"
          >
            <Icon name="ph:exam-fill" class="text-xl" />
          </div>
          <div>
            <h2 class="text-sm font-extrabold text-slate-900">
              Level-Up Exam: B1 → B2
            </h2>
            <p class="text-xs text-slate-500">
              Section {{ currentSection + 1 }} of {{ sections.length }}
            </p>
          </div>
        </div>

        <!-- Timer -->
        <div
          :class="[
            'flex items-center gap-3 px-5 py-2 rounded-full font-extrabold text-lg',
            timeRemaining <= 120
              ? 'bg-red-100 text-red-700 border border-red-200'
              : timeRemaining <= 600
                ? 'bg-amber-100 text-amber-700 border border-amber-200'
                : 'bg-slate-100 text-slate-800 border border-slate-200',
          ]"
        >
          <Icon name="ph:timer-fill" class="text-xl" />
          {{ formatTime(timeRemaining) }}
        </div>

        <!-- Section Progress -->
        <div class="flex items-center gap-2">
          <div
            v-for="(sec, i) in sections"
            :key="i"
            :class="[
              'w-8 h-8 rounded-lg flex items-center justify-center text-xs font-bold transition-all',
              i < currentSection
                ? 'bg-emerald-500 text-white'
                : i === currentSection
                  ? 'bg-indigo-500 text-white shadow-md shadow-indigo-500/30'
                  : 'bg-slate-100 text-slate-400 border border-slate-200',
            ]"
          >
            <Icon v-if="i < currentSection" name="ph:check-bold" />
            <span v-else>{{ i + 1 }}</span>
          </div>
        </div>
      </header>

      <!-- Exam Content Area -->
      <main class="flex-1 flex items-center justify-center p-8 overflow-auto">
        <div class="w-full max-w-3xl">
          <!-- Section: Grammar MCQ -->
          <div v-if="currentSection === 0" class="space-y-8 animate-float-up">
            <div class="text-center mb-8">
              <Icon
                name="ph:brain-fill"
                class="text-4xl text-indigo-500 mb-3"
              />
              <h2 class="text-2xl font-extrabold text-slate-900">
                Section 1: Grammar
              </h2>
              <p class="text-slate-500 mt-1">
                Choose the correct answer for each question.
              </p>
            </div>

            <div
              v-for="(q, qi) in grammarQuestions"
              :key="qi"
              class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm"
            >
              <p class="text-sm font-bold text-slate-400 mb-2">
                Question {{ qi + 1 }}
              </p>
              <p class="text-lg font-semibold text-slate-800 mb-5">
                {{ q.question }}
              </p>
              <div class="grid grid-cols-2 gap-3">
                <button
                  v-for="(opt, oi) in q.options"
                  :key="oi"
                  @click="q.selected = oi"
                  :class="[
                    'p-4 rounded-2xl border-2 text-left text-sm font-medium transition-all',
                    q.selected === oi
                      ? 'border-indigo-500 bg-indigo-50 text-indigo-700 shadow-md'
                      : 'border-slate-200 bg-slate-50 text-slate-600 hover:border-slate-300 hover:bg-white',
                  ]"
                >
                  <span class="font-bold mr-2"
                    >{{ String.fromCharCode(65 + oi) }}.</span
                  >
                  {{ opt }}
                </button>
              </div>
            </div>
          </div>

          <!-- Section: Reading Comprehension -->
          <div v-if="currentSection === 1" class="space-y-8 animate-float-up">
            <div class="text-center mb-8">
              <Icon
                name="ph:book-open-text-fill"
                class="text-4xl text-purple-500 mb-3"
              />
              <h2 class="text-2xl font-extrabold text-slate-900">
                Section 2: Reading Comprehension
              </h2>
              <p class="text-slate-500 mt-1">
                Read the passage and answer the questions.
              </p>
            </div>

            <div
              class="bg-white rounded-3xl border border-slate-200 p-8 shadow-sm mb-6"
            >
              <p class="text-slate-700 leading-[1.9] text-[15px]">
                The concept of remote work has fundamentally changed the modern
                workplace. Companies that once required employees to commute
                daily now embrace flexible schedules. Studies show that remote
                workers report higher job satisfaction and, in many cases,
                increased productivity. However, challenges persist: feelings of
                isolation, difficulty separating work from personal life, and
                communication barriers remain common concerns.
              </p>
            </div>

            <div
              v-for="(q, qi) in readingQuestions"
              :key="qi"
              class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm"
            >
              <p class="text-sm font-bold text-slate-400 mb-2">
                Question {{ qi + 1 }}
              </p>
              <p class="text-lg font-semibold text-slate-800 mb-5">
                {{ q.question }}
              </p>
              <div class="space-y-3">
                <button
                  v-for="(opt, oi) in q.options"
                  :key="oi"
                  @click="q.selected = oi"
                  :class="[
                    'w-full p-4 rounded-2xl border-2 text-left text-sm font-medium transition-all',
                    q.selected === oi
                      ? 'border-indigo-500 bg-indigo-50 text-indigo-700 shadow-md'
                      : 'border-slate-200 bg-slate-50 text-slate-600 hover:border-slate-300 hover:bg-white',
                  ]"
                >
                  {{ opt }}
                </button>
              </div>
            </div>
          </div>

          <!-- Section: Writing -->
          <div v-if="currentSection === 2" class="space-y-6 animate-float-up">
            <div class="text-center mb-8">
              <Icon
                name="ph:pencil-fill"
                class="text-4xl text-emerald-500 mb-3"
              />
              <h2 class="text-2xl font-extrabold text-slate-900">
                Section 3: Writing
              </h2>
              <p class="text-slate-500 mt-1">
                Write a short essay. Minimum 100 words.
              </p>
            </div>

            <div class="bg-indigo-50 rounded-2xl p-5 border border-indigo-100">
              <p class="text-sm font-bold text-indigo-800 mb-1">Prompt:</p>
              <p class="text-indigo-700 leading-relaxed">
                "Do you think working from home is better than working in an
                office? Discuss the advantages and disadvantages."
              </p>
            </div>

            <textarea
              v-model="writingAnswer"
              placeholder="Write your essay here..."
              class="w-full h-64 bg-white border-2 border-slate-200 rounded-2xl p-6 text-slate-700 text-[15px] leading-[1.9] resize-none focus:outline-none focus:border-indigo-500 transition-all shadow-inner"
            ></textarea>
            <p class="text-sm text-slate-500 text-right">
              Word count:
              <strong
                :class="
                  examWritingWordCount >= 100
                    ? 'text-emerald-600'
                    : 'text-amber-600'
                "
                >{{ examWritingWordCount }}</strong
              >/100
            </p>
          </div>

          <!-- Section: AI Live Conversation (Grand Finale) -->
          <div v-if="currentSection === 3" class="space-y-6 animate-float-up">
            <div class="text-center mb-8">
              <div
                class="w-20 h-20 rounded-full bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center mx-auto shadow-xl shadow-indigo-500/30 mb-4"
                :class="{ 'buddy-pulse': isExamRecording }"
              >
                <Icon name="ph:robot-fill" class="text-white text-4xl" />
              </div>
              <h2 class="text-2xl font-extrabold text-slate-900">
                Section 4: Live AI Conversation
              </h2>
              <p class="text-slate-500 mt-1">
                2-minute live conversation with your AI examiner
              </p>
            </div>

            <div
              class="bg-white rounded-3xl border border-slate-200 shadow-sm overflow-hidden"
            >
              <div
                class="p-6 space-y-4 max-h-64 overflow-y-auto custom-scrollbar"
              >
                <div
                  v-for="(msg, i) in examChat"
                  :key="i"
                  :class="[
                    'flex gap-3',
                    msg.role === 'user' ? 'justify-end' : '',
                  ]"
                >
                  <div
                    v-if="msg.role === 'ai'"
                    class="w-8 h-8 rounded-full bg-indigo-100 flex items-center justify-center text-indigo-600 shrink-0"
                  >
                    <Icon name="ph:robot-fill" />
                  </div>
                  <div
                    :class="[
                      'max-w-[70%] p-4 rounded-2xl text-sm',
                      msg.role === 'ai'
                        ? 'bg-slate-50 border border-slate-200 text-slate-700 rounded-tl-sm'
                        : 'bg-indigo-600 text-white rounded-tr-sm',
                    ]"
                  >
                    {{ msg.text }}
                  </div>
                </div>
              </div>

              <div
                class="p-6 border-t border-slate-100 flex items-center gap-4"
              >
                <button
                  @click="isExamRecording = !isExamRecording"
                  :class="[
                    'w-14 h-14 rounded-full flex items-center justify-center text-xl transition-all shadow-lg',
                    isExamRecording
                      ? 'bg-red-500 text-white buddy-pulse shadow-red-500/30'
                      : 'bg-gradient-to-br from-indigo-500 to-purple-600 text-white hover:scale-105',
                  ]"
                >
                  <Icon
                    :name="
                      isExamRecording ? 'ph:stop-fill' : 'ph:microphone-fill'
                    "
                  />
                </button>
                <input
                  v-model="examInput"
                  @keydown.enter="sendExamMessage"
                  type="text"
                  placeholder="Speak or type your answer..."
                  class="flex-1 bg-slate-50 border-2 border-slate-200 rounded-xl py-3 px-5 text-sm focus:outline-none focus:border-indigo-500 transition"
                />
                <button
                  @click="sendExamMessage"
                  class="w-12 h-12 rounded-xl bg-indigo-500 text-white flex items-center justify-center hover:bg-indigo-600 transition"
                >
                  <Icon name="ph:paper-plane-right-fill" />
                </button>
              </div>
            </div>
          </div>

          <!-- Navigation Buttons -->
          <div class="flex justify-between mt-10">
            <button
              v-if="currentSection > 0"
              @click="currentSection--"
              class="px-6 py-3 rounded-xl bg-white border border-slate-200 text-slate-700 font-semibold hover:bg-slate-50 transition flex items-center gap-2 shadow-sm"
            >
              <Icon name="ph:arrow-left" /> Previous
            </button>
            <div v-else></div>

            <button
              v-if="currentSection < sections.length - 1"
              @click="currentSection++"
              class="px-6 py-3 rounded-xl bg-indigo-600 text-white font-semibold hover:bg-indigo-700 transition flex items-center gap-2 shadow-md"
            >
              Next Section <Icon name="ph:arrow-right" />
            </button>
            <button
              v-else
              @click="finishExam"
              class="px-8 py-3.5 rounded-xl bg-gradient-to-r from-emerald-500 to-emerald-600 text-white font-bold hover:shadow-xl hover:shadow-emerald-500/30 transition-all flex items-center gap-2 text-lg glow-button"
            >
              <Icon name="ph:flag-checkered-fill" /> Finish Exam
            </button>
          </div>
        </div>
      </main>
    </template>

    <!-- Results Screen (with Confetti!) -->
    <div
      v-if="examFinished"
      class="flex-1 flex items-center justify-center relative overflow-hidden"
    >
      <!-- Confetti Pieces -->
      <template v-if="passed">
        <div
          v-for="i in 60"
          :key="'confetti-' + i"
          class="confetti-piece rounded-sm"
          :style="{
            left: Math.random() * 100 + '%',
            width: Math.random() * 10 + 5 + 'px',
            height: Math.random() * 10 + 5 + 'px',
            backgroundColor: confettiColors[i % confettiColors.length],
            '--fall-dur': Math.random() * 2 + 2 + 's',
            '--fall-delay': Math.random() * 1.5 + 's',
          }"
        ></div>
      </template>

      <div class="max-w-lg text-center px-6 relative z-10 animate-float-up">
        <!-- Pass -->
        <template v-if="passed">
          <div class="text-7xl mb-6">🎉</div>
          <h1
            class="text-5xl font-extrabold text-slate-900 tracking-tight mb-3"
          >
            Congratulations!
          </h1>
          <p class="text-xl text-slate-600 mb-2">You've officially reached</p>
          <div
            class="inline-flex items-center gap-3 bg-gradient-to-r from-indigo-500 to-purple-600 text-white px-8 py-4 rounded-2xl text-2xl font-extrabold shadow-xl shadow-indigo-500/30 mb-8"
          >
            <Icon name="ph:trophy-fill" class="text-amber-300 text-3xl" />
            B2 — Upper Intermediate
          </div>
        </template>

        <!-- Fail -->
        <template v-else>
          <div class="text-7xl mb-6">📚</div>
          <h1
            class="text-4xl font-extrabold text-slate-900 tracking-tight mb-3"
          >
            Almost there!
          </h1>
          <p class="text-xl text-slate-600 mb-2">
            Keep practicing — you're close to advancing
          </p>
          <div
            class="inline-flex items-center gap-3 bg-slate-100 text-slate-700 px-8 py-4 rounded-2xl text-xl font-extrabold border border-slate-200 mb-8"
          >
            Stay at B1 — Try again soon
          </div>
        </template>

        <!-- Score Breakdown -->
        <div
          class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm text-left mb-8"
        >
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-5 text-center"
          >
            Score Breakdown
          </h3>
          <div class="space-y-4">
            <div
              v-for="sec in resultSections"
              :key="sec.label"
              class="flex items-center gap-4"
            >
              <div
                class="w-10 h-10 rounded-xl flex items-center justify-center shrink-0 border"
                :class="sec.bg"
              >
                <Icon :name="sec.icon" class="text-xl" />
              </div>
              <div class="flex-1">
                <div class="flex justify-between mb-1">
                  <span class="text-sm font-semibold text-slate-700">{{
                    sec.label
                  }}</span>
                  <span
                    class="text-sm font-extrabold"
                    :class="
                      sec.score >= 70 ? 'text-emerald-600' : 'text-red-500'
                    "
                    >{{ sec.score }}%</span
                  >
                </div>
                <div class="h-2 bg-slate-100 rounded-full overflow-hidden">
                  <div
                    class="h-full rounded-full transition-all duration-1000"
                    :class="sec.score >= 70 ? 'bg-emerald-500' : 'bg-red-400'"
                    :style="{ width: sec.score + '%' }"
                  ></div>
                </div>
              </div>
            </div>
          </div>
          <div
            class="mt-6 pt-5 border-t border-slate-100 flex justify-between items-center"
          >
            <span class="text-lg font-extrabold text-slate-900"
              >Total Score</span
            >
            <span
              class="text-3xl font-extrabold"
              :class="passed ? 'text-emerald-600' : 'text-red-500'"
              >{{ totalScore }}%</span
            >
          </div>
        </div>

        <div class="flex gap-4 justify-center">
          <NuxtLink
            to="/learn/dashboard"
            class="px-8 py-3.5 rounded-xl bg-slate-900 text-white font-bold hover:bg-slate-800 transition shadow-lg"
          >
            Back to Dashboard
          </NuxtLink>
          <button
            v-if="!passed"
            @click="retryExam"
            class="px-8 py-3.5 rounded-xl bg-indigo-600 text-white font-bold hover:bg-indigo-700 transition shadow-lg"
          >
            Try Again
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: false });

// State
const examStarted = ref(false);
const examFinished = ref(false);
const currentSection = ref(0);
const timeRemaining = ref(30 * 60); // 30 mins
const writingAnswer = ref("");
const examInput = ref("");
const isExamRecording = ref(false);

const sections = ["Grammar", "Reading", "Writing", "AI Speaking"];

const confettiColors = [
  "#6366f1",
  "#a855f7",
  "#ec4899",
  "#f59e0b",
  "#10b981",
  "#3b82f6",
  "#ef4444",
];

// Timer
let timerInterval = null;

function startExam() {
  examStarted.value = true;
  timerInterval = setInterval(() => {
    if (timeRemaining.value > 0) {
      timeRemaining.value--;
    } else {
      finishExam();
    }
  }, 1000);
}

function formatTime(sec) {
  const m = Math.floor(sec / 60);
  const s = sec % 60;
  return `${m.toString().padStart(2, "0")}:${s.toString().padStart(2, "0")}`;
}

// Grammar MCQ
const grammarQuestions = ref([
  {
    question: "She _____ to the office every day before the pandemic.",
    options: ["commuted", "has commuted", "commutes", "is commuting"],
    selected: null,
    correct: 0,
  },
  {
    question: "If I _____ more time, I would study abroad.",
    options: ["have", "had", "will have", "having"],
    selected: null,
    correct: 1,
  },
  {
    question: "The report _____ by the manager last Friday.",
    options: ["was reviewed", "reviewed", "is reviewed", "has reviewed"],
    selected: null,
    correct: 0,
  },
]);

// Reading MCQ
const readingQuestions = ref([
  {
    question: "What is the main topic of the passage?",
    options: [
      "The history of office work",
      "The impact of remote work on the modern workplace",
      "How to increase productivity",
      "The downsides of technology",
    ],
    selected: null,
    correct: 1,
  },
  {
    question:
      "Which of the following is NOT mentioned as a challenge of remote work?",
    options: [
      "Feeling isolated",
      "Communication barriers",
      "Lower salary",
      "Difficulty separating work and personal life",
    ],
    selected: null,
    correct: 2,
  },
]);

// Exam Writing word count
const examWritingWordCount = computed(() => {
  return writingAnswer.value.trim()
    ? writingAnswer.value.trim().split(/\s+/).length
    : 0;
});

// Exam Chat
const examChat = ref([
  {
    role: "ai",
    text: "Hello! I'm your AI examiner. Let's have a natural conversation. Tell me about a skill you've recently learned and why it's important to you.",
  },
]);

function sendExamMessage() {
  if (!examInput.value.trim()) return;
  examChat.value.push({ role: "user", text: examInput.value });
  examInput.value = "";
  setTimeout(() => {
    examChat.value.push({
      role: "ai",
      text: "That's interesting! Can you explain how you practiced that skill and what challenges you faced during the learning process?",
    });
  }, 1500);
}

// Results
const resultSections = ref([
  {
    label: "Grammar",
    score: 85,
    icon: "ph:brain-fill",
    bg: "bg-indigo-100 text-indigo-600 border-indigo-200",
  },
  {
    label: "Reading",
    score: 78,
    icon: "ph:book-open-text-fill",
    bg: "bg-purple-100 text-purple-600 border-purple-200",
  },
  {
    label: "Writing",
    score: 72,
    icon: "ph:pencil-fill",
    bg: "bg-emerald-100 text-emerald-600 border-emerald-200",
  },
  {
    label: "AI Speaking",
    score: 80,
    icon: "ph:microphone-fill",
    bg: "bg-amber-100 text-amber-600 border-amber-200",
  },
]);

const totalScore = computed(() => {
  const avg =
    resultSections.value.reduce((sum, s) => sum + s.score, 0) /
    resultSections.value.length;
  return Math.round(avg);
});

const passed = computed(() => totalScore.value >= 70);

function finishExam() {
  if (timerInterval) clearInterval(timerInterval);
  examFinished.value = true;
}

function retryExam() {
  examFinished.value = false;
  examStarted.value = false;
  currentSection.value = 0;
  timeRemaining.value = 30 * 60;
  writingAnswer.value = "";
  grammarQuestions.value.forEach((q) => (q.selected = null));
  readingQuestions.value.forEach((q) => (q.selected = null));
  examChat.value = [
    {
      role: "ai",
      text: "Hello! I'm your AI examiner. Let's have a natural conversation. Tell me about a skill you've recently learned and why it's important to you.",
    },
  ];
}

onUnmounted(() => {
  if (timerInterval) clearInterval(timerInterval);
});
</script>
