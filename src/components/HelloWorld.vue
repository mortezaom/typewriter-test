<template>
  <div class="greetings">
    <h1 class="green">{{ typer }}<span></span> </h1>
    <h3>
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const { msg } = defineProps<{
  msg: string
}>()
const typer = ref(msg)
const data = {
  texts: ['Hello World!', 'This is a typewriter animation!', 'It is created with Vue 3 and Vite!'],
}

// create a typewriter function
const createTyper = (text: string, i = 0, fnCallback?: () => void) => {
  if (i < (text.length)) {
    typer.value = text.substring(0, i + 1);

    setTimeout(() => {
      createTyper(text, i + 1, fnCallback)
    }, 150);
  } else if (typeof fnCallback == 'function') {
    setTimeout(fnCallback, 1500);
  }
}
// start a typewriter animation for a text in the data.texts array
const startTextAnimation = (i: number) => {
  if (typeof data.texts[i] == 'undefined') {
    setTimeout(() => {
      startTextAnimation(0);
    }, 10000);
  }
  // check if data.texts[i] exists
  else {
    // text exists! start typewriter animation
    createTyper(data.texts[i], 0, () => {
      startTextAnimation(i + 1);
    });
  }
}
// start the text animation
startTextAnimation(0);
</script>


<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}

.green {
  position: relative;
  display: inline-block;
}

.green span::after {
  /* Characters: ︳ , _ */
  content: "_";
  font-family: 'Times New Roman', Times, serif !important;
  animation: blink 0.6s ease-in-out infinite;
}

@keyframes blink {
  0% {
    opacity: 0;
  }

  50% {
    opacity: 1;
  }

  100% {
    opacity: 0;
  }
}
</style>
