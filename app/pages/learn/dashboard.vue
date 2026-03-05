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

    <!-- Top Stats Row with Sparklines -->
    <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-6">
      <div
        v-for="stat in topStats"
        :key="stat.label"
        class="bg-white rounded-3xl border border-slate-200 p-6 shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all duration-300 relative overflow-hidden group"
      >
        <div class="flex items-center justify-between mb-2">
          <div
            :class="[
              'w-10 h-10 rounded-xl flex items-center justify-center border',
              stat.colorClass,
            ]"
          >
            <Icon :name="stat.icon" class="text-xl" />
          </div>
          <span
            v-if="stat.trend"
            class="text-[10px] font-bold text-emerald-600 bg-emerald-50 px-2.5 py-1 rounded-full border border-emerald-100"
            >{{ stat.trend }}</span
          >
        </div>
        <div class="relative z-10">
          <p class="text-xs font-bold text-slate-400 uppercase tracking-wider">
            {{ stat.label }}
          </p>
          <p class="text-3xl font-black text-slate-900 mt-1">
            {{ stat.value }}
          </p>
        </div>

        <!-- Sparkline Background -->
        <div
          class="absolute bottom-0 left-0 right-0 h-16 opacity-20 pointer-events-none group-hover:opacity-40 transition-opacity"
        >
          <svg
            class="w-full h-full"
            viewBox="0 0 100 40"
            preserveAspectRatio="none"
          >
            <path
              :d="stat.sparkline"
              fill="none"
              :stroke="stat.strokeColor"
              stroke-width="2"
              stroke-linecap="round"
            />
          </svg>
        </div>
      </div>
    </div>

    <!-- ========== TOPIC MASTERY BREAKDOWN ========== -->
    <div class="grid lg:grid-cols-3 gap-8">
      <div
        class="lg:col-span-2 bg-white rounded-[2.5rem] border border-slate-200 p-8 shadow-sm relative overflow-hidden"
      >
        <div class="flex items-center justify-between mb-8">
          <div>
            <h2 class="text-xl font-extrabold text-slate-900 tracking-tight">
              Topic Mastery Breakdown
            </h2>
            <p class="text-sm text-slate-500 font-medium">
              Visual distribution of your learning skills
            </p>
          </div>
          <div class="flex items-center gap-2">
            <div
              class="flex items-center gap-1.5 px-3 py-1.5 rounded-full bg-slate-50 border border-slate-100"
            >
              <div class="w-2 h-2 rounded-full bg-indigo-500"></div>
              <span class="text-[10px] font-bold text-slate-500 uppercase"
                >Tenses</span
              >
            </div>
            <div
              class="flex items-center gap-1.5 px-3 py-1.5 rounded-full bg-slate-50 border border-slate-100"
            >
              <div class="w-2 h-2 rounded-full bg-purple-500"></div>
              <span class="text-[10px] font-bold text-slate-500 uppercase"
                >Grammar</span
              >
            </div>
          </div>
        </div>

        <!-- Mastery Bar Chart -->
        <div class="h-64 flex items-end justify-between gap-4 py-4 px-2">
          <div
            v-for="bar in masteryBars"
            :key="bar.label"
            class="flex-1 flex flex-col items-center group"
          >
            <div
              class="relative w-full flex flex-col items-center h-full justify-end"
            >
              <!-- Bar -->
              <div
                class="w-full max-w-[40px] rounded-t-xl transition-all duration-500 group-hover:brightness-110 relative"
                :style="{ height: bar.height + 'px', background: bar.color }"
              >
                <!-- Tooltip -->
                <div
                  class="absolute -top-10 left-1/2 -translate-x-1/2 bg-slate-900 text-white text-[10px] font-bold py-1 px-2 rounded-lg opacity-0 group-hover:opacity-100 transition-opacity whitespace-nowrap z-20 shadow-xl"
                >
                  {{ bar.percent }}% Complete
                </div>
              </div>
            </div>
            <span
              class="text-[10px] font-bold text-slate-400 mt-4 uppercase rotate-[-45deg] lg:rotate-0 tracking-tighter"
              >{{ bar.label }}</span
            >
          </div>
        </div>
      </div>

      <!-- Quick Learning Card -->
      <div
        class="bg-gradient-to-br from-indigo-600 to-purple-700 rounded-[2.5rem] p-8 text-white relative overflow-hidden group h-full"
      >
        <div
          class="absolute -right-10 -bottom-10 w-40 h-40 bg-white/10 rounded-full blur-3xl group-hover:scale-125 transition-transform duration-700"
        ></div>
        <div class="relative z-10 flex flex-col h-full">
          <div
            class="w-12 h-12 rounded-2xl bg-white/20 backdrop-blur border border-white/20 flex items-center justify-center mb-6"
          >
            <Icon name="ph:lightning-fill" class="text-2xl" />
          </div>
          <h3 class="text-2xl font-black mb-2">Daily Goal</h3>
          <p class="text-indigo-100 text-sm font-medium mb-8 leading-relaxed">
            Your radar shows <strong>Reading</strong> and
            <strong>Writing</strong> need focus today.
          </p>

          <div class="space-y-3 mb-8">
            <div
              v-for="(task, i) in dailyTasks"
              :key="i"
              class="flex items-center gap-3 p-3 rounded-2xl bg-white/10 border border-white/10"
            >
              <div
                class="w-7 h-7 rounded-lg bg-emerald-400 text-slate-900 flex items-center justify-center text-xs font-black"
              >
                <Icon v-if="task.done" name="ph:check-bold" />
                <span v-else>{{ i + 1 }}</span>
              </div>
              <p class="text-xs font-bold">{{ task.label }}</p>
            </div>
          </div>

          <button
            class="mt-auto w-full py-4 rounded-2xl bg-white text-indigo-600 font-extrabold hover:bg-slate-50 transition active:scale-95 shadow-xl"
          >
            Continue Learning
          </button>
        </div>
      </div>
    </div>

    <!-- Main Dashboard Grid -->
    <div class="grid lg:grid-cols-3 gap-8">
      <!-- Left Column: Activity Chart -->
      <div
        class="bg-white rounded-[2.5rem] border border-slate-200 p-8 shadow-sm"
      >
        <h3
          class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-8"
        >
          Activity Intensity
        </h3>
        <div class="relative h-48 w-full group">
          <!-- Activity Line Chart -->
          <svg
            class="w-full h-full"
            viewBox="0 0 300 100"
            preserveAspectRatio="none"
          >
            <defs>
              <linearGradient
                id="areaGradient"
                x1="0%"
                y1="0%"
                x2="0%"
                y2="100%"
              >
                <stop offset="0%" stop-color="#6366f1" stop-opacity="0.2" />
                <stop offset="100%" stop-color="#6366f1" stop-opacity="0" />
              </linearGradient>
            </defs>
            <path :d="activityAreaPath" fill="url(#areaGradient)" />
            <path
              :d="activityLinePath"
              fill="none"
              stroke="#6366f1"
              stroke-width="3"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <!-- Dots -->
            <circle
              v-for="(pt, i) in activityPoints"
              :key="i"
              :cx="pt.x"
              :cy="pt.y"
              r="4"
              fill="white"
              stroke="#6366f1"
              stroke-width="2"
              class="hover:r-6 cursor-pointer"
            />
          </svg>
        </div>
        <div class="flex justify-between mt-4">
          <span
            v-for="day in weekData"
            :key="day.label"
            class="text-[10px] font-bold text-slate-400 uppercase"
            >{{ day.label }}</span
          >
        </div>
        <div
          class="mt-8 pt-8 border-t border-slate-100 flex items-center justify-between"
        >
          <div>
            <p
              class="text-xs font-bold text-slate-400 uppercase tracking-wider"
            >
              Total Time
            </p>
            <p class="text-xl font-black text-slate-900 mt-1">32.5h</p>
          </div>
          <div>
            <p
              class="text-xs font-bold text-slate-400 uppercase tracking-wider"
            >
              Avg Session
            </p>
            <p class="text-xl font-black text-slate-900 mt-1">45m</p>
          </div>
        </div>
      </div>

      <!-- Center Column: Skill Radar Chart -->
      <div
        class="bg-white rounded-[2.5rem] border border-slate-200 p-8 shadow-sm"
      >
        <h3
          class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-6"
        >
          Skill Portfolio
        </h3>
        <div class="flex justify-center">
          <svg viewBox="0 0 300 300" class="w-full max-w-[240px]">
            <polygon
              v-for="level in [1, 0.75, 0.5, 0.25]"
              :key="level"
              :points="pentagonPoints(150, 150, 120 * level)"
              fill="none"
              stroke="#f1f5f9"
              stroke-width="1.5"
            />
            <line
              v-for="(_, i) in skills"
              :key="'axis-' + i"
              x1="150"
              y1="150"
              :x2="getRadarPoint(150, 150, 120, i, skills.length).x"
              :y2="getRadarPoint(150, 150, 120, i, skills.length).y"
              stroke="#f1f5f9"
              stroke-width="1.5"
            />
            <polygon
              :points="radarDataPoints"
              fill="rgba(99,102,241,0.12)"
              stroke="#6366f1"
              stroke-width="3"
              stroke-linejoin="round"
            />
            <circle
              v-for="(skill, i) in skills"
              :key="'pt-' + i"
              :cx="
                getRadarPoint(150, 150, 120 * skill.value, i, skills.length).x
              "
              :cy="
                getRadarPoint(150, 150, 120 * skill.value, i, skills.length).y
              "
              r="6"
              fill="#6366f1"
              stroke="white"
              stroke-width="2.5"
            />
            <text
              v-for="(skill, i) in skills"
              :key="'lbl-' + i"
              :x="getRadarPoint(150, 150, 140, i, skills.length).x"
              :y="getRadarPoint(150, 150, 140, i, skills.length).y"
              text-anchor="middle"
              dominant-baseline="middle"
              class="fill-slate-500 text-[11px] font-bold"
            >
              {{ skill.label }}
            </text>
          </svg>
        </div>
      </div>

      <!-- Right Column: Progress Ring -->
      <div
        class="bg-white rounded-[2.5rem] border border-slate-200 p-8 shadow-sm text-center flex flex-col items-center justify-center"
      >
        <h3
          class="text-sm font-bold text-slate-400 uppercase tracking-widest mb-10"
        >
          Milestone Progress
        </h3>
        <div class="relative inline-flex items-center justify-center">
          <svg class="w-48 h-48" viewBox="0 0 200 200">
            <circle
              cx="100"
              cy="100"
              r="85"
              fill="none"
              stroke="#f1f5f9"
              stroke-width="16"
            />
            <circle
              cx="100"
              cy="100"
              r="85"
              fill="none"
              stroke="url(#progressGradient)"
              stroke-width="16"
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
            <span class="text-xs font-bold text-indigo-600 mt-1"
              >B1 INTERMEDIATE</span
            >
          </div>
        </div>
        <p class="text-xs font-medium text-slate-500 mt-10 max-w-[180px]">
          You're <strong>320 XP</strong> away from reaching
          <strong>B2 Upper Intermediate</strong>.
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: "learn" });

const progressPercent = ref(68);
const circumference = 2 * Math.PI * 85;

// Unified Stats with Sparklines
const topStats = ref([
  {
    label: "Lessons Completed",
    value: "47",
    icon: "ph:target-fill",
    colorClass: "bg-indigo-50 text-indigo-600 border-indigo-100",
    strokeColor: "#6366f1",
    trend: "+12%",
    sparkline: "M0 30 Q15 20 30 25 T60 10 T100 20",
  },
  {
    label: "Study Time",
    value: "32.5h",
    icon: "ph:clock-fill",
    colorClass: "bg-purple-50 text-purple-600 border-purple-100",
    strokeColor: "#a855f7",
    trend: "+5h",
    sparkline: "M0 35 L20 25 L40 30 L60 15 L80 20 L100 5",
  },
  {
    label: "Current Streak",
    value: "12d",
    icon: "ph:flame-fill",
    colorClass: "bg-amber-50 text-amber-600 border-amber-100",
    strokeColor: "#f59e0b",
    sparkline: "M0 40 C20 40 30 10 50 10 C70 10 80 40 100 40",
  },
  {
    label: "Words Mastered",
    value: "1.2k",
    icon: "ph:brain-fill",
    colorClass: "bg-emerald-50 text-emerald-600 border-emerald-100",
    strokeColor: "#10b981",
    sparkline: "M0 30 Q25 5 50 30 T100 10",
  },
]);

// Mastery Bars Data
const masteryBars = ref([
  { label: "Present Tense", height: 120, percent: 85, color: "#6366f1" },
  { label: "Past Tense", height: 140, percent: 95, color: "#6366f1" },
  { label: "Future Tense", height: 80, percent: 55, color: "#6366f1" },
  { label: "Modals", height: 100, percent: 70, color: "#a855f7" },
  { label: "Articles", height: 130, percent: 88, color: "#a855f7" },
  { label: "Passives", height: 60, percent: 42, color: "#a855f7" },
  { label: "Daily Vocab", height: 150, percent: 100, color: "#10b981" },
  { label: "Tech Vocab", height: 90, percent: 62, color: "#10b981" },
]);

const dailyTasks = ref([
  { label: "5min Speaking", xp: "+20", icon: "ph:microphone", done: true },
  { label: "Vocabulary Set", xp: "+15", icon: "ph:book-open", done: true },
  { label: "Read Article", xp: "+25", icon: "ph:article", done: false },
  { label: "Grammar Quiz", xp: "+30", icon: "ph:brain", done: false },
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
  { label: "Thu", mins: 5 },
  { label: "Fri", mins: 35 },
  { label: "Sat", mins: 10 },
  { label: "Sun", mins: 0 },
]);

// Activity Chart Logic
const activityPoints = computed(() => {
  const maxMins = 50;
  return weekData.value.map((d, i) => ({
    x: (i * 300) / 6,
    y: 100 - (d.mins / maxMins) * 80 - 10,
  }));
});

const activityLinePath = computed(() => {
  const points = activityPoints.value;
  if (!points.length) return "";
  let path = `M ${points[0].x} ${points[0].y}`;
  for (let i = 1; i < points.length; i++) {
    const prev = points[i - 1];
    const curr = points[i];
    const cp1x = prev.x + (curr.x - prev.x) / 2;
    path += ` C ${cp1x} ${prev.y} ${cp1x} ${curr.y} ${curr.x} ${curr.y}`;
  }
  return path;
});

const activityAreaPath = computed(() => {
  const line = activityLinePath.value;
  if (!line) return "";
  return `${line} L 300 100 L 0 100 Z`;
});

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
