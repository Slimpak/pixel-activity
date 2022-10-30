<template>
  <div class="main">
    <div class="tools">
      <!-- <button @click="toggleShow()">
        Show
      </button> -->
    </div>
      <main class="content">
        <h1>Activity in my heart:</h1>
        <dashBoard>
        </dashBoard>
      </main>
  </div>
</template>

<script>
import { ref } from 'vue';

import dashboard from './components/dashboard.vue'

export default {
  name: 'App',
  components: {
    dashBoard: dashboard,
  },
  setup() {
    const isShow = ref(false);

    function toggleShow() {
      isShow.value = !isShow.value
    }

    return {
      isShow,
        toggleShow
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
