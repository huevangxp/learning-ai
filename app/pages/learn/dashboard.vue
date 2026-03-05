<template>
  <div class="space-y-8">
    <!-- Welcome Header -->
    <div
      class="flex flex-col lg:flex-row lg:items-center justify-between gap-4"
    >
      <div>
        <h1 class="text-3xl font-extrabold text-slate-900 tracking-tight">
          Good morning, John! 👋
        </h1>
        <p class="text-slate-500 mt-1">
          You're on a 12-day streak. Keep the momentum going!
        </p>
      </div>
      <div class="flex gap-3">
        <button
          class="px-5 py-2.5 bg-white border border-slate-200 text-slate-700 rounded-xl text-sm font-semibold hover:bg-slate-50 transition shadow-sm flex items-center gap-2"
        >
          <Icon name="ph:calendar" class="text-lg" /> Daily Path
        </button>
        <button
          @click="navigateTo('/learn/speaking')"
          class="px-5 py-2.5 bg-gradient-to-r from-indigo-600 to-purple-600 text-white rounded-xl text-sm font-bold hover:shadow-lg hover:shadow-indigo-500/20 transition-all shadow-md flex items-center gap-2"
        >
          <Icon name="ph:play-fill" /> Continue Learning
        </button>
      </div>
    </div>

    <!-- Top Stats Row -->
    <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-6">
      <div
        class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all duration-300"
      >
        <div class="flex items-center justify-between mb-4">
          <div
            class="w-12 h-12 rounded-2xl bg-indigo-100 text-indigo-600 flex items-center justify-center border border-indigo-200"
          >
            <Icon name="ph:target-fill" class="text-2xl" />
          </div>
          <span
            class="text-xs font-bold text-emerald-600 bg-emerald-50 px-2.5 py-1 rounded-full border border-emerald-100"
            >+12%</span
          >
        </div>
        <p class="text-sm font-medium text-slate-500">Lessons Completed</p>
        <p class="text-3xl font-extrabold text-slate-900 mt-1">47</p>
      </div>
      <div
        class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all duration-300"
      >
        <div class="flex items-center justify-between mb-4">
          <div
            class="w-12 h-12 rounded-2xl bg-purple-100 text-purple-600 flex items-center justify-center border border-purple-200"
          >
            <Icon name="ph:clock-fill" class="text-2xl" />
          </div>
          <span
            class="text-xs font-bold text-emerald-600 bg-emerald-50 px-2.5 py-1 rounded-full border border-emerald-100"
            >+5h</span
          >
        </div>
        <p class="text-sm font-medium text-slate-500">Study Time</p>
        <p class="text-3xl font-extrabold text-slate-900 mt-1">32.5h</p>
      </div>
      <div
        class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all duration-300"
      >
        <div class="flex items-center justify-between mb-4">
          <div
            class="w-12 h-12 rounded-2xl bg-amber-100 text-amber-600 flex items-center justify-center border border-amber-200"
          >
            <Icon name="ph:flame-fill" class="text-2xl" />
          </div>
        </div>
        <p class="text-sm font-medium text-slate-500">Current Streak</p>
        <p
          class="text-3xl font-extrabold text-slate-900 mt-1 flex items-center gap-2"
        >
          12 <span class="text-base font-medium text-slate-400">days</span>
        </p>
      </div>
      <div
        class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all duration-300"
      >
        <div class="flex items-center justify-between mb-4">
          <div
            class="w-12 h-12 rounded-2xl bg-emerald-100 text-emerald-600 flex items-center justify-center border border-emerald-200"
          >
            <Icon name="ph:brain-fill" class="text-2xl" />
          </div>
        </div>
        <p class="text-sm font-medium text-slate-500">Words Mastered</p>
        <p class="text-3xl font-extrabold text-slate-900 mt-1">1,284</p>
      </div>
    </div>

    <!-- Main Dashboard Grid -->
    <div class="grid lg:grid-cols-3 gap-8">
      <!-- Left Column: Progress Ring + Daily Path -->
      <div class="space-y-6">
        <!-- Progress Ring Card -->
        <div
          class="bg-white rounded-3xl border border-slate-200 p-8 shadow-sm text-center"
        >
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-6"
          >
            Level Progress
          </h3>
          <div class="relative inline-flex items-center justify-center">
            <svg class="w-48 h-48" viewBox="0 0 200 200">
              <circle
                cx="100"
                cy="100"
                r="85"
                fill="none"
                stroke="#e2e8f0"
                stroke-width="12"
              />
              <circle
                cx="100"
                cy="100"
                r="85"
                fill="none"
                stroke="url(#progressGradient)"
                stroke-width="12"
                stroke-linecap="round"
                class="progress-ring-circle"
                :stroke-dasharray="circumference"
                :stroke-dashoffset="
                  circumference - (circumference * progressPercent) / 100
                "
              />
              <defs>
                <linearGradient
                  id="progressGradient"
                  x1="0%"
                  y1="0%"
                  x2="100%"
                  y2="100%"
                >
                  <stop offset="0%" stop-color="#6366f1" />
                  <stop offset="100%" stop-color="#a855f7" />
                </linearGradient>
              </defs>
            </svg>
            <div
              class="absolute inset-0 flex flex-col items-center justify-center"
            >
              <span class="text-5xl font-extrabold text-slate-900"
                >{{ progressPercent }}%</span
              >
              <span class="text-sm font-semibold text-indigo-600 mt-1"
                >B1 → B2</span
              >
            </div>
          </div>
          <p class="text-sm text-slate-500 mt-4">
            320 XP more to reach
            <strong class="text-slate-800">B2 Intermediate</strong>
          </p>

          <!-- Exam Ready Glow Button -->
          <button
            v-if="progressPercent >= 90"
            @click="navigateTo('/learn/exam')"
            class="mt-6 w-full py-3.5 rounded-2xl bg-gradient-to-r from-indigo-500 to-purple-600 text-white font-bold glow-button transition-all hover:-translate-y-0.5"
          >
            🎯 Take Level-Up Exam
          </button>
        </div>

        <!-- Daily Goals Checklist -->
        <div class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm">
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-5"
          >
            Today's Daily Path
          </h3>
          <div class="space-y-3">
            <div
              v-for="(task, i) in dailyTasks"
              :key="i"
              :class="[
                'flex items-center gap-4 p-3.5 rounded-2xl border transition-all cursor-pointer',
                task.done
                  ? 'bg-emerald-50/50 border-emerald-100'
                  : 'bg-slate-50 border-slate-100 hover:bg-slate-100',
              ]"
              @click="task.done = !task.done"
            >
              <div
                :class="[
                  'w-8 h-8 rounded-full flex items-center justify-center shrink-0 transition-all text-sm font-bold',
                  task.done
                    ? 'bg-emerald-500 text-white'
                    : 'bg-white border-2 border-slate-300 text-slate-400',
                ]"
              >
                <Icon v-if="task.done" name="ph:check-bold" />
                <span v-else>{{ i + 1 }}</span>
              </div>
              <div class="flex-1">
                <p
                  :class="[
                    'text-sm font-semibold',
                    task.done
                      ? 'text-emerald-700 line-through'
                      : 'text-slate-700',
                  ]"
                >
                  {{ task.label }}
                </p>
                <p class="text-[11px] text-slate-400 mt-0.5">
                  {{ task.xp }} XP
                </p>
              </div>
              <Icon
                :name="task.icon"
                :class="[
                  'text-xl',
                  task.done ? 'text-emerald-500' : 'text-slate-400',
                ]"
              />
            </div>
          </div>
        </div>
      </div>

      <!-- Center Column: Skill Radar + Recommended -->
      <div class="space-y-6">
        <!-- Skill Radar Chart (Pentagon) -->
        <div class="bg-white rounded-3xl border border-slate-200 p-8 shadow-sm">
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-6"
          >
            Skill Radar
          </h3>
          <div class="flex justify-center">
            <svg viewBox="0 0 300 300" class="w-full max-w-[280px]">
              <!-- Pentagon Grid Lines -->
              <polygon
                v-for="level in [1, 0.75, 0.5, 0.25]"
                :key="level"
                :points="pentagonPoints(150, 150, 120 * level)"
                fill="none"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <!-- Axes -->
              <line
                v-for="(_, i) in skills"
                :key="'axis-' + i"
                x1="150"
                y1="150"
                :x2="getRadarPoint(150, 150, 120, i, skills.length).x"
                :y2="getRadarPoint(150, 150, 120, i, skills.length).y"
                stroke="#e2e8f0"
                stroke-width="1"
              />
              <!-- Filled Area -->
              <polygon
                :points="radarDataPoints"
                fill="rgba(99,102,241,0.15)"
                stroke="#6366f1"
                stroke-width="2.5"
              />
              <!-- Data Points -->
              <circle
                v-for="(skill, i) in skills"
                :key="'pt-' + i"
                :cx="
                  getRadarPoint(150, 150, 120 * skill.value, i, skills.length).x
                "
                :cy="
                  getRadarPoint(150, 150, 120 * skill.value, i, skills.length).y
                "
                r="5"
                fill="#6366f1"
                stroke="white"
                stroke-width="2"
              />
              <!-- Labels -->
              <text
                v-for="(skill, i) in skills"
                :key="'lbl-' + i"
                :x="getRadarPoint(150, 150, 140, i, skills.length).x"
                :y="getRadarPoint(150, 150, 140, i, skills.length).y"
                text-anchor="middle"
                dominant-baseline="middle"
                class="fill-slate-600 text-[11px] font-semibold"
              >
                {{ skill.label }}
              </text>
            </svg>
          </div>
          <div class="mt-4 flex flex-wrap justify-center gap-3">
            <div
              v-for="skill in skills"
              :key="skill.label"
              class="flex items-center gap-1.5 text-xs text-slate-500 bg-slate-50 px-3 py-1.5 rounded-full border border-slate-100"
            >
              <span class="w-2 h-2 rounded-full bg-indigo-500"></span>
              {{ skill.label }}: {{ Math.round(skill.value * 100) }}%
            </div>
          </div>
        </div>

        <!-- Weekly Activity Heatmap -->
        <div class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm">
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-5"
          >
            This Week
          </h3>
          <div class="grid grid-cols-7 gap-2">
            <div v-for="(day, i) in weekData" :key="i" class="text-center">
              <p class="text-[10px] text-slate-400 font-bold mb-2">
                {{ day.label }}
              </p>
              <div
                :class="[
                  'w-full aspect-square rounded-xl flex items-center justify-center text-xs font-bold transition-all',
                  day.mins === 0
                    ? 'bg-slate-100 text-slate-300'
                    : day.mins < 15
                      ? 'bg-indigo-100 text-indigo-600'
                      : day.mins < 30
                        ? 'bg-indigo-200 text-indigo-700'
                        : 'bg-indigo-500 text-white shadow-md',
                ]"
              >
                {{ day.mins > 0 ? day.mins + "m" : "—" }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Right Column: Achievements + Leaderboard -->
      <div class="space-y-6">
        <!-- Recent Achievements -->
        <div class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm">
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-5"
          >
            Achievements
          </h3>
          <div class="space-y-3">
            <div
              v-for="badge in badges"
              :key="badge.title"
              class="flex items-center gap-4 p-3 rounded-2xl bg-slate-50 border border-slate-100 hover:bg-white hover:shadow-md transition-all"
            >
              <div
                class="w-12 h-12 rounded-xl flex items-center justify-center text-2xl shrink-0"
                :class="badge.bg"
              >
                {{ badge.emoji }}
              </div>
              <div class="flex-1 min-w-0">
                <p class="text-sm font-bold text-slate-800">
                  {{ badge.title }}
                </p>
                <p class="text-[11px] text-slate-400 truncate">
                  {{ badge.desc }}
                </p>
              </div>
              <Icon
                name="ph:check-circle-fill"
                class="text-emerald-500 text-xl shrink-0"
              />
            </div>
          </div>
        </div>

        <!-- Mini Leaderboard -->
        <div
          class="bg-gradient-to-b from-slate-900 to-slate-800 rounded-3xl p-6 shadow-xl text-white border border-slate-700"
        >
          <h3
            class="text-sm font-bold text-slate-300 uppercase tracking-widest mb-5 flex items-center gap-2"
          >
            <Icon name="ph:trophy-fill" class="text-amber-400 text-lg" />
            Leaderboard
          </h3>
          <div class="space-y-3">
            <div
              v-for="(user, i) in leaderboard"
              :key="i"
              :class="[
                'flex items-center gap-3 p-3 rounded-xl transition-all',
                i === 2
                  ? 'bg-indigo-500/20 border border-indigo-500/30'
                  : 'bg-white/5',
              ]"
            >
              <span
                :class="[
                  'w-7 h-7 rounded-lg flex items-center justify-center text-xs font-extrabold shrink-0',
                  i === 0
                    ? 'bg-amber-400 text-amber-900'
                    : i === 1
                      ? 'bg-slate-300 text-slate-700'
                      : 'bg-indigo-500 text-white',
                ]"
              >
                {{ i + 1 }}
              </span>
              <div
                class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center text-[10px] font-bold border border-slate-600"
              >
                {{ user.avatar }}
              </div>
              <div class="flex-1 min-w-0">
                <p
                  class="text-sm font-bold truncate"
                  :class="i === 2 ? 'text-indigo-300' : ''"
                >
                  {{ user.name }}
                  <span v-if="i === 2" class="text-xs text-indigo-400"
                    >(You)</span
                  >
                </p>
              </div>
              <span class="text-sm font-extrabold text-slate-300">{{
                user.xp
              }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: "learn" });

const progressPercent = ref(68);
const circumference = 2 * Math.PI * 85;

const dailyTasks = ref([
  {
    label: "Practice 5 mins Speaking",
    xp: "+20",
    icon: "ph:microphone",
    done: true,
  },
  {
    label: "Complete Vocabulary Set",
    xp: "+15",
    icon: "ph:book-open",
    done: true,
  },
  { label: "Read a short article", xp: "+25", icon: "ph:article", done: false },
  { label: "Grammar Quick Quiz", xp: "+30", icon: "ph:brain", done: false },
]);

const skills = ref([
  { label: "Speaking", value: 0.72 },
  { label: "Listening", value: 0.85 },
  { label: "Reading", value: 0.65 },
  { label: "Writing", value: 0.58 },
  { label: "Grammar", value: 0.78 },
]);

const weekData = ref([
  { label: "Mon", mins: 45 },
  { label: "Tue", mins: 30 },
  { label: "Wed", mins: 20 },
  { label: "Thu", mins: 0 },
  { label: "Fri", mins: 35 },
  { label: "Sat", mins: 10 },
  { label: "Sun", mins: 0 },
]);

const badges = ref([
  {
    emoji: "🔥",
    title: "7-Day Streak",
    desc: "Study 7 consecutive days",
    bg: "bg-orange-100",
  },
  {
    emoji: "🎯",
    title: "First Exam",
    desc: "Passed your first level test",
    bg: "bg-indigo-100",
  },
  {
    emoji: "💬",
    title: "AI Chatter",
    desc: "50 conversations with AI tutor",
    bg: "bg-purple-100",
  },
]);

const leaderboard = ref([
  { name: "Sarah K.", avatar: "SK", xp: "4,820" },
  { name: "Miguel R.", avatar: "MR", xp: "3,910" },
  { name: "John Doe", avatar: "JD", xp: "2,450" },
  { name: "Yuki T.", avatar: "YT", xp: "2,100" },
]);

// Radar Chart Helpers
function getRadarPoint(cx, cy, r, index, total) {
  const angle = (Math.PI * 2 * index) / total - Math.PI / 2;
  return { x: cx + r * Math.cos(angle), y: cy + r * Math.sin(angle) };
}

function pentagonPoints(cx, cy, r) {
  return Array.from({ length: 5 }, (_, i) => {
    const pt = getRadarPoint(cx, cy, r, i, 5);
    return `${pt.x},${pt.y}`;
  }).join(" ");
}

const radarDataPoints = computed(() => {
  return skills.value
    .map((s, i) => {
      const pt = getRadarPoint(150, 150, 120 * s.value, i, skills.value.length);
      return `${pt.x},${pt.y}`;
    })
    .join(" ");
});
</script>
