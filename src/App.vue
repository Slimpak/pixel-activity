<template>
  <div class="main">
    <div class="tools">
      <toolsWrapper
        v-model:colors="colorsArray"
        v-model:title="title"
      />
      <!-- <button @click="toggleShow()">
        Show
      </button> -->
    </div>
      <main class="content">
        <h1>{{ title }}:</h1>
        <dashBoard>
        </dashBoard>
      </main>
  </div>
</template>

<script>
import { ref, provide } from 'vue';

import dashboard from './components/dashboard.vue'
import toolsWrapper from './components/tools/toolsWrapper.vue'

const COLORS = [
  '#9be9a8;',
  '#40c463',
  '#216e39',
]

export default {
  name: 'App',
  components: {
    dashBoard: dashboard,
    toolsWrapper,
  },
  setup() {
    const colorsArray = ref(COLORS);
    const isShow = ref(false);
    const title = ref('Hello');

    function toggleShow() {
      isShow.value = !isShow.value
    }

    provide('arrayColors', colorsArray.value)

    return {
      isShow,
        toggleShow,
        colorsArray,
        title
    };
  },
}
</script>

<style>

* {
  box-sizing: border-box;
  font-family: monospace;
  margin: 0;
}

.main {
  align-items: center;
  background: #1e1e1e;
  color: #fff;
  display: flex;
  height: 100vh;
  justify-content: center;
  padding: 0;
  width: 100vw;
}

.content {
  background: rgb(0 0 0 / 82%);
  border-radius: 4px;
  padding: 10px;
}
</style>
