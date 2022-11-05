<template>
  <div class="main">
    <div class="tools">
      <toolsWrapper
        v-model:colors="colorsArray"
        v-model:title="title"
        v-model:countYears="countYears"
        @draw="drawMode()"
        @activeColor="activeColor($event)"
        @reset="resetToBlack()"
        @fill="fillColors()"
      />
    </div>
    <main class="content">
      <h1>{{ title }}:</h1>
      <dashBoard
        :count-years="Number(countYears)"
      />
    </main>
  </div>
</template>

<script>
import { ref, provide } from 'vue';

import dashboard from './components/dashboard.vue';
import toolsWrapper from './components/tools/toolsWrapper.vue';

const COLORS = [
  '#ebedf0',
  '#9be9a8',
  '#40c463',
  '#30a14e',
  '#216e39',
];

export default {
  name: 'App',
  components: {
    dashBoard: dashboard,
    toolsWrapper,
  },
  setup() {
    const colorsArray = ref(COLORS);
    const isShow = ref(false);
    const title = ref('My Activity');
    const countYears = ref(3);
    const triggerClear = ref({ status: false });
    const fillColorsTrigger = ref({ status: false });
    const activeDraw = ref({ status: false });
    const indexColorDraw = ref({ index: 0 });

    function drawMode() {
      console.log('drawMode', !activeDraw.value);
      activeDraw.value.status = !activeDraw.value.status;
    }

    function resetToBlack() {
      console.log('resetToBlack', !triggerClear.value);
      triggerClear.value.status = !triggerClear.value.status;
    }

    function toggleShow() {
      isShow.value = !isShow.value;
    }

    function activeColor(value) {
      console.log(value);
      indexColorDraw.value.index = value;
      console.log('indexColorDraw.value', indexColorDraw.value);
    }

    function fillColors() {
      console.log('resetToBlack', !triggerClear.value);
      fillColorsTrigger.value.status = !fillColorsTrigger.value.status;
    }

    provide('arrayColors', colorsArray.value);
    provide('provideTriggerClear', triggerClear.value);
    provide('provideTriggerFill', fillColorsTrigger.value);
    provide('provideActiveDraw', activeDraw.value);
    provide('provideIndexColorDraw', indexColorDraw.value);

    return {
      activeColor,
      isShow,
      fillColors,
      drawMode,
      toggleShow,
      colorsArray,
      title,
      countYears,
      resetToBlack,
      activeDraw,
      indexColorDraw,
    };
  },
};
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
