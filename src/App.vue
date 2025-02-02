<script lang="ts" setup>
import {ref, watch} from "vue";
import NumberFlow from '@number-flow/vue'
import InfoBlock from "./components/InfoBlock.vue";
import { ArrowUp, Brain, Code, Bug, Shield, AlertCircle } from "lucide-vue-next";


const infoBlocks = [

  {
    title: "Типизация",
    mainText: "Чел... в XXI веке с динамической типизацией",
    icon: Brain,
  },
  {
    title: "Баги JS",
    mainText: "undefined is not a function...",
    icon: Bug,
  },
  {
    title: "Безопасность",
    mainText: "TS ловит ошибки до запуска, а не в проде",
    icon: Shield,
  },
  {
    title: "Код читабельный",
    mainText: "TS-код = сразу понятно, что происходит",
    icon: Code,
  },
  {
    title: "JS боль",
    mainText: "У всех глаза высыхают, когда видят файлы с расширением .js",
    icon: AlertCircle,
  },
  {
    title: "JavaScript говно",
    mainText: "Реально говно - это общепринятый факт",
    icon: ArrowUp,
  },
];

const gayTheme = ref(false);
const tsAge = ref(0);

function calculateTypescriptAge(): number {
  const creationDate = new Date(2012, 9, 1);
  const currentDate = new Date();
  const diffMs = currentDate.getTime() - creationDate.getTime();
  const msPerYear = 1000 * 60 * 60 * 24 * 365.25;

  const years = diffMs / msPerYear;
  return Number(years.toFixed(10));
}

watch(gayTheme, ()=>{
  if (gayTheme.value) {
    document.getElementById('tswins')?.classList.add('gay')
    return
  }
  document.getElementById('tswins')?.classList.remove('gay')

})

setInterval(() => {
  tsAge.value = calculateTypescriptAge();
},50);
</script>


<template>
  <button @click="gayTheme = !gayTheme" class="ml-4 mb-4 absolute bottom-0 left-0 text-sm p-2 rounded-2xl border border-slate-400">
    {{!gayTheme ? 'Enable' : 'Disable'}} furry theme
  </button>
  <div class="flex p-16 flex-col items-center align-center gap-10">
    <h1 id="tswins" class="tswins font-bold text-5xl">TS победа уже</h1>
    <div>
      <NumberFlow
          class="text-6xl"
          :value="tsAge"
          :format="{ minimumFractionDigits: 8, maximumFractionDigits: 8 }"
      />
      <span class="text-3xl opacity-45">лет</span>
    </div>

    <div class="grid mt-10 md:grid-cols-2 lg:grid-cols-3 sm:grid-cols-1 gap-4">
      <InfoBlock
          v-for="(block, index) in infoBlocks"
          :key="index"
          :title="block.title"
          :mainText="block.mainText"
      >
        <component :is="block.icon" />
      </InfoBlock>
    </div>


  </div>
</template>

<style scoped>

.tswins.gay{
  animation: colorFlow 3s infinite alternate;
}

@keyframes colorFlow {
  0% { color: red; }
  20% { color: orange; }
  40% { color: yellow; }
  60% { color: green; }
  80% { color: blue; }
  100% { color: purple; }
}

</style>