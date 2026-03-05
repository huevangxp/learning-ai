<template>
  <div class="h-[calc(100vh-64px)] flex flex-col overflow-hidden">
    <!-- Top Bar -->
    <div
      class="shrink-0 flex items-center justify-between px-6 py-3 bg-white border-b border-slate-200"
    >
      <div class="flex items-center gap-4">
        <h2 class="text-lg font-extrabold text-slate-900">
          Reading & Writing Workspace
        </h2>
        <span
          class="bg-purple-100 text-purple-700 text-xs font-bold px-3 py-1 rounded-full border border-purple-200"
        >
          Lesson: Climate Change
        </span>
      </div>
      <div class="flex items-center gap-3 text-sm">
        <div
          class="flex items-center gap-2 px-4 py-2 bg-emerald-50 border border-emerald-100 rounded-xl text-emerald-700 font-bold"
        >
          <Icon name="ph:timer" class="text-lg" /> 12:30 spent
        </div>
        <button
          class="px-4 py-2 rounded-xl bg-indigo-600 text-white font-semibold hover:bg-indigo-700 transition shadow-md flex items-center gap-2"
        >
          <Icon name="ph:paper-plane-right-fill" /> Submit Work
        </button>
      </div>
    </div>

    <!-- Split Screen Content -->
    <div class="flex-1 flex overflow-hidden relative">
      <!-- LEFT: Reading Pane -->
      <div class="w-1/2 border-r border-slate-200 flex flex-col bg-white">
        <div
          class="px-6 py-4 border-b border-slate-100 bg-slate-50 flex items-center justify-between shrink-0"
        >
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest flex items-center gap-2"
          >
            <Icon
              name="ph:book-open-text-fill"
              class="text-indigo-500 text-lg"
            />
            Source Text
          </h3>
          <div class="flex gap-2">
            <button
              @click="fontSize = Math.max(12, fontSize - 1)"
              class="w-8 h-8 rounded-lg bg-white border border-slate-200 text-slate-500 flex items-center justify-center hover:bg-slate-100 transition text-xs font-bold"
            >
              A-
            </button>
            <button
              @click="fontSize = Math.min(22, fontSize + 1)"
              class="w-8 h-8 rounded-lg bg-white border border-slate-200 text-slate-500 flex items-center justify-center hover:bg-slate-100 transition text-xs font-bold"
            >
              A+
            </button>
          </div>
        </div>

        <div
          class="flex-1 overflow-y-auto p-8 custom-scrollbar"
          @mouseup="handleTextSelection"
        >
          <article
            :style="{ fontSize: fontSize + 'px' }"
            class="text-slate-700 leading-[1.9] space-y-5 max-w-prose"
          >
            <h2
              class="text-2xl font-extrabold text-slate-900 !leading-tight mb-2"
            >
              The Effects of Climate Change on Coastal Communities
            </h2>

            <p>
              <span class="text-indigo-600 font-bold">Climate change</span> is
              one of the most
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('pressing', $event)"
                >pressing</span
              >
              challenges of our time. Rising sea levels,
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('exacerbated', $event)"
                >exacerbated</span
              >
              by the melting of polar ice caps, threaten
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('coastal', $event)"
                >coastal</span
              >
              cities around the world.
            </p>

            <p>
              In the past decade, scientists have observed a
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('significant', $event)"
                >significant</span
              >
              increase in the frequency of extreme weather events. Hurricanes,
              flooding, and droughts are becoming more
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('prevalent', $event)"
                >prevalent</span
              >, causing billions of dollars in damage.
            </p>

            <p>
              The
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('displacement', $event)"
                >displacement</span
              >
              of communities is perhaps the most tragic consequence. As farmland
              turns arid and oceans rise, millions may need to relocate,
              creating a new class of "climate refugees."
            </p>

            <p>
              However, there is hope. Renewable energy solutions, conservation
              efforts, and international
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('cooperation', $event)"
                >cooperation</span
              >
              can mitigate the worst effects. The Paris Agreement, signed by
              nearly every nation, represents a
              <span
                class="bg-amber-100 px-1 rounded cursor-pointer hover:bg-amber-200 transition"
                @click="showWordPopup('collective', $event)"
                >collective</span
              >
              commitment to reducing carbon emissions.
            </p>

            <div
              class="mt-8 bg-indigo-50 border border-indigo-100 rounded-2xl p-5"
            >
              <h4
                class="text-sm font-bold text-indigo-800 mb-2 flex items-center gap-2"
              >
                <Icon name="ph:lightbulb-fill" class="text-amber-500" />
                Vocabulary in Context
              </h4>
              <p class="text-sm text-indigo-700 leading-relaxed">
                Highlighted words are key vocabulary. Click on any highlighted
                word to see its definition, translation, or usage in other
                sentences.
              </p>
            </div>
          </article>
        </div>
      </div>

      <!-- RIGHT: Writing Pane -->
      <div class="w-1/2 flex flex-col bg-slate-50">
        <div
          class="px-6 py-4 border-b border-slate-100 bg-white flex items-center justify-between shrink-0"
        >
          <h3
            class="text-sm font-bold text-slate-400 uppercase tracking-widest flex items-center gap-2"
          >
            <Icon name="ph:pencil-fill" class="text-purple-500 text-lg" /> Your
            Response
          </h3>
          <div class="flex items-center gap-2 text-xs text-slate-500">
            <span
              :class="[
                'font-bold',
                wordCount >= 150 ? 'text-emerald-600' : 'text-slate-500',
              ]"
              >{{ wordCount }}/200 words</span
            >
            <span
              v-if="wordCount >= 150"
              class="text-emerald-500 flex items-center gap-1"
              ><Icon name="ph:check-circle-fill" /> Target reached!</span
            >
          </div>
        </div>

        <!-- Writing Prompt -->
        <div
          class="px-6 py-4 bg-gradient-to-r from-purple-50 to-indigo-50 border-b border-slate-100 shrink-0"
        >
          <div class="flex items-start gap-3">
            <div
              class="w-10 h-10 rounded-xl bg-purple-100 text-purple-600 flex items-center justify-center shrink-0 border border-purple-200"
            >
              <Icon name="ph:chat-teardrop-text-fill" class="text-xl" />
            </div>
            <div>
              <p class="text-sm font-bold text-purple-900">Writing Prompt:</p>
              <p class="text-sm text-purple-700 mt-1 leading-relaxed">
                Summarize the main argument of the article and discuss one
                solution you would propose to help coastal communities. Use at
                least 3 vocabulary words from the text.
              </p>
            </div>
          </div>
        </div>

        <!-- Text Area -->
        <div class="flex-1 p-6 overflow-y-auto">
          <textarea
            v-model="writingInput"
            placeholder="Start writing your response here..."
            class="w-full h-full bg-white border-2 border-slate-200 rounded-2xl p-6 text-slate-700 text-[15px] leading-[1.9] resize-none focus:outline-none focus:border-indigo-500 focus:bg-white transition-all shadow-inner placeholder-slate-300"
          ></textarea>
        </div>

        <!-- AI Feedback Bar -->
        <div class="shrink-0 border-t border-slate-200 bg-white p-4">
          <div
            v-if="aiFeedback"
            class="bg-emerald-50 border border-emerald-200 rounded-2xl p-4 flex items-start gap-3 animate-float-up"
          >
            <div
              class="w-10 h-10 rounded-xl bg-emerald-100 text-emerald-600 flex items-center justify-center shrink-0 border border-emerald-200"
            >
              <Icon name="ph:robot-fill" class="text-xl" />
            </div>
            <div class="flex-1">
              <p
                class="text-xs font-bold text-emerald-800 uppercase tracking-widest mb-1"
              >
                AI Writing Feedback
              </p>
              <p class="text-sm text-emerald-700 leading-relaxed">
                {{ aiFeedback }}
              </p>
            </div>
            <button
              @click="aiFeedback = ''"
              class="text-emerald-400 hover:text-emerald-600 transition"
            >
              <Icon name="ph:x" class="text-lg" />
            </button>
          </div>
          <div class="flex items-center gap-3 mt-3">
            <button
              @click="getAiFeedback"
              class="flex-1 py-3 rounded-xl bg-gradient-to-r from-indigo-500 to-purple-500 text-white text-sm font-bold hover:shadow-lg hover:shadow-indigo-500/20 transition-all flex items-center justify-center gap-2"
            >
              <Icon name="ph:robot" class="text-lg" /> Get AI Feedback
            </button>
            <button
              class="px-4 py-3 rounded-xl bg-slate-100 text-slate-600 text-sm font-semibold hover:bg-slate-200 transition border border-slate-200"
            >
              <Icon name="ph:eraser" class="text-lg" />
            </button>
          </div>
        </div>
      </div>

      <!-- AI Context Popup (for selected/clicked words) -->
      <Transition name="popup">
        <div
          v-if="wordPopup.show"
          class="absolute z-50 bg-white border border-slate-200 rounded-2xl shadow-2xl p-5 w-80 animate-float-up"
          :style="{ top: wordPopup.y + 'px', left: wordPopup.x + 'px' }"
        >
          <div class="flex items-center justify-between mb-3">
            <h4 class="text-lg font-extrabold text-slate-900">
              {{ wordPopup.word }}
            </h4>
            <button
              @click="wordPopup.show = false"
              class="text-slate-400 hover:text-slate-600 transition"
            >
              <Icon name="ph:x" class="text-lg" />
            </button>
          </div>
          <div class="space-y-3">
            <div class="flex items-start gap-2">
              <Icon
                name="ph:book-open"
                class="text-indigo-500 text-lg mt-0.5 shrink-0"
              />
              <div>
                <p
                  class="text-xs font-bold text-slate-400 uppercase tracking-wider"
                >
                  Definition
                </p>
                <p class="text-sm text-slate-700 mt-0.5">
                  {{
                    wordDefinitions[wordPopup.word]?.definition || "Loading..."
                  }}
                </p>
              </div>
            </div>
            <div class="flex items-start gap-2">
              <Icon
                name="ph:translate"
                class="text-purple-500 text-lg mt-0.5 shrink-0"
              />
              <div>
                <p
                  class="text-xs font-bold text-slate-400 uppercase tracking-wider"
                >
                  Translation
                </p>
                <p class="text-sm text-slate-700 mt-0.5">
                  {{ wordDefinitions[wordPopup.word]?.translation || "..." }}
                </p>
              </div>
            </div>
            <div class="flex items-start gap-2">
              <Icon
                name="ph:chat-text"
                class="text-emerald-500 text-lg mt-0.5 shrink-0"
              />
              <div>
                <p
                  class="text-xs font-bold text-slate-400 uppercase tracking-wider"
                >
                  Use in a Sentence
                </p>
                <p class="text-sm text-slate-700 mt-0.5 italic">
                  {{ wordDefinitions[wordPopup.word]?.sentence || "..." }}
                </p>
              </div>
            </div>
          </div>
          <button
            class="mt-4 w-full py-2.5 bg-indigo-50 text-indigo-700 rounded-xl text-sm font-semibold hover:bg-indigo-100 transition border border-indigo-100 flex items-center justify-center gap-2"
          >
            <Icon name="ph:plus" /> Add to Vocabulary List
          </button>
        </div>
      </Transition>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: "learn" });

const fontSize = ref(16);
const writingInput = ref("");
const aiFeedback = ref("");

const wordCount = computed(() => {
  return writingInput.value.trim()
    ? writingInput.value.trim().split(/\s+/).length
    : 0;
});

const wordPopup = reactive({
  show: false,
  word: "",
  x: 0,
  y: 0,
});

const wordDefinitions = {
  pressing: {
    definition: "Requiring immediate attention; urgent.",
    translation: "เร่งด่วน / urgente",
    sentence: '"This is a pressing matter that cannot wait until tomorrow."',
  },
  exacerbated: {
    definition: "Made a problem or situation worse.",
    translation: "ทำให้แย่ลง / aggravated",
    sentence: '"The drought was exacerbated by years of deforestation."',
  },
  coastal: {
    definition: "Relating to or near the coast.",
    translation: "ชายฝั่ง / côtier",
    sentence: '"Coastal cities face the greatest risk from rising sea levels."',
  },
  significant: {
    definition: "Large enough to be noticed or have an effect; important.",
    translation: "สำคัญ / significativo",
    sentence:
      '"There has been a significant improvement in her English skills."',
  },
  prevalent: {
    definition: "Widespread in a particular area or at a particular time.",
    translation: "แพร่หลาย / predominante",
    sentence:
      '"Fast food has become increasingly prevalent in modern society."',
  },
  displacement: {
    definition: "The forced movement of people from their homes.",
    translation: "การอพยพ / desplazamiento",
    sentence:
      '"The flooding caused the displacement of thousands of residents."',
  },
  cooperation: {
    definition: "The process of working together to achieve the same goal.",
    translation: "ความร่วมมือ / cooperación",
    sentence:
      '"International cooperation is essential to solving global challenges."',
  },
  collective: {
    definition: "Done by people acting as a group.",
    translation: "ร่วมกัน / collectif",
    sentence: '"The team made a collective decision to change their strategy."',
  },
};

function showWordPopup(word, event) {
  const rect = event.target.getBoundingClientRect();
  const container = event.target.closest(".flex-1.flex");
  const containerRect = container?.getBoundingClientRect() || {
    top: 0,
    left: 0,
  };

  wordPopup.word = word;
  wordPopup.x = Math.min(
    rect.left - containerRect.left,
    window.innerWidth - 350,
  );
  wordPopup.y = rect.bottom - containerRect.top + 8;
  wordPopup.show = true;
}

function handleTextSelection() {
  const selection = window.getSelection();
  if (selection && selection.toString().trim().length > 2) {
    const word = selection.toString().trim().toLowerCase();
    if (wordDefinitions[word]) {
      const range = selection.getRangeAt(0);
      const rect = range.getBoundingClientRect();
      const container = document.querySelector(".flex-1.flex");
      const containerRect = container?.getBoundingClientRect() || {
        top: 0,
        left: 0,
      };
      wordPopup.word = word;
      wordPopup.x = Math.min(
        rect.left - containerRect.left,
        window.innerWidth - 350,
      );
      wordPopup.y = rect.bottom - containerRect.top + 8;
      wordPopup.show = true;
    }
  }
}

function getAiFeedback() {
  if (!writingInput.value.trim()) {
    aiFeedback.value =
      "Please write something first so I can provide feedback!";
    return;
  }
  aiFeedback.value =
    "Good structure! Your summary captures the main points well. Consider using the word 'exacerbated' to strengthen your second paragraph. Also, try replacing 'very important' with 'significant' — it sounds more academic. Your proposed solution about renewable energy is thoughtful but could use a specific example.";
}
</script>

<style scoped>
.popup-enter-active {
  transition: all 0.2s ease-out;
}
.popup-leave-active {
  transition: all 0.15s ease-in;
}
.popup-enter-from,
.popup-leave-to {
  opacity: 0;
  transform: translateY(8px) scale(0.95);
}
</style>
