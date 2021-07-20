<script setup lang="ts">

const pastWork = [
  {
    title: 'Thesis',
    subtitle: 'Thesis in Computer Science',
    path: '/thesis/',
  },
  {
    title: 'Thesis2',
    subtitle: 'Thesis in Computer Science',
    path: '/thesis/',
  },
  {
    title: 'Thesis3',
    subtitle: 'Thesis in Computer Science',
    path: '/thesis/',
  },
  {
    title: 'Thesis4',
    subtitle: 'Thesis in Computer Science',
    path: '/thesis/',
  },
  {
    title: 'Thesis5',
    subtitle: 'Thesis in Computer Science',
    path: '/thesis/',
  },
  {
    title: 'Thesis6',
    subtitle: 'Thesis in Computer Science',
    path: '/thesis/',
  },
]

const text = ref('Samuel Vallonfrontend developer')
const typedTitle = ref('')
const typedSubTitle = ref('')
const nextLetter = ref('')
const charIndex = ref(0)
const pagination = ref(1)
const transitionDirection = ref('moveup')

watch(pagination, (val, bef) => {
  if (val < bef) transitionDirection.value = 'movedown'
  if (val > bef) transitionDirection.value = 'moveup'
})

function sleep(ms: any) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function typeText(text: any) {
  if (charIndex.value < 1) await sleep(800)
  if (charIndex.value < text.length) {
    if (text[charIndex.value] === ' ') {
      if (typedTitle.value.length < 13) typedTitle.value = typedTitle.value + text[charIndex.value]
      else typedSubTitle.value = typedSubTitle.value + text[charIndex.value]
      charIndex.value++
      typeText(text)
      return
    }
    nextLetter.value = text[charIndex.value]
    await sleep(70)
    nextLetter.value = ''
    if (typedTitle.value.length < 13) typedTitle.value = typedTitle.value + text[charIndex.value]
    else typedSubTitle.value = typedSubTitle.value + text[charIndex.value]
    charIndex.value++

    nextTick(() => typeText(text))
  }
}

typeText(text.value)

</script>

<template>
  <div class="flex flex-col h-screen justify-center md:items-center text-xl md:flex-row" @keyup.up="1 !== pagination ? pagination-- : null" @keyup.down="pastWork.length !== pagination * 2 ? pagination++ : null">
    <div class="h-20 md:w-1/2">
      <h1 class="text-[2.2rem] md:text-[2.4rem] text-left font-medium tracking-wide">
        {{ typedTitle }}<transition name="fade">
          <span v-if="nextLetter && typedTitle.length < 13" class="text-teal-600">{{ nextLetter }}</span>
        </transition>
      </h1>
      <div class="text-2xl mt-2 md:mt-3 text-left  dark:text-teal-600 dark:opacity-60" :class="{'dark:opacity-100': typedSubTitle.length === 18}">
        {{ typedSubTitle }}<transition name="fade">
          <span v-if="nextLetter && typedSubTitle.length > 0" class="dark:text-gray-300 text-gray-500">{{ nextLetter }}</span>
        </transition>
      </div>
    </div>
    <div class="mt-10 h-60 md:w-1/2 relative">
      <div v-for="(work, i) in pastWork" :key="i">
        <div class="relative transform hover:scale-102 transition-transform ease-in">
          <transition :name="transitionDirection">
            <main-card v-if="pagination * 2 - 2 < i + 1 && pagination * 2 > i && text.length === charIndex" :title="work.title" class="absolute" :class="{'top-30': i % 2}" />
          </transition>
        </div>
      </div>

      <transition name="fadein">
        <div v-if="text.length === charIndex">
          <button class="absolute -top-10 left-51 icon-btn" @click="1 !== pagination ? pagination-- : null">
            <fa:angle-double-left class="transform rotate-90 mr-2 ml-1 mt-1 mb-0" />
          </button>
          <button class="absolute -bottom-8 left-[12.6rem] icon-btn" @click="pastWork.length !== pagination * 2 ? pagination++ : null">
            <fa:angle-double-left class="transform rotate-270 mr-2 ml-1 mt-1 mb-0" />
          </button>
        </div>
      </transition>
    </div>
  </div>
  <div class="h-12">
    <transition name="fadein">
      <Footer v-if="text.length === charIndex" class="mb-0 mt-auto w-full" />
    </transition>
  </div>
</template>

<style>
.fade-enter-active {
  transition: opacity 0.07s ease;
}
.fade-enter-from, .fade-leave-from {
  opacity: 0;
}

.fadein-enter-active {
  transition: opacity 3s ease;
}
.fadein-enter-from {
  opacity: 0;
}

.moveup-enter-active {
  transition: all 0.8s ease;
}
.moveup-enter-from {
  opacity: 0;
  transform: translateY(60px);
}
.moveup-leave-active {
  transition: all 0.3s ease;
}
.moveup-leave-to {
  opacity: 0;
  transform: translateY(-90px);
}

.movedown-enter-active {
  transition: all 0.8s ease;
}
.movedown-enter-from {
  opacity: 0;
  transform: translateY(-60px);
}
.movedown-leave-active {
  transition: all 0.3s ease;
}
.movedown-leave-to {
  opacity: 0;
  transform: translateY(90px);
}
</style>
