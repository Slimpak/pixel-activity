<template>
  <div
    class="day"
    :style="`background: ${ getColor };`"
    @click="addActivity()"
    @mouseover="handleEvent"
  />
</template>

<script>
import {
  ref, computed, inject, watch,
} from 'vue';

export default {
  name: 'DayItem',
  setup() {
    const userClick = ref(false);
    const clear = inject('provideTriggerClear', ref([]));
    const colors = inject('arrayColors', ref([]));
    const fill = inject('provideTriggerFill', ref([]));
    const drawMode = inject('provideActiveDraw', ref([]));
    const indexColorDraw = inject('provideIndexColorDraw', ref([]));
    const idColor = ref(Math.floor(Math.random() * colors.length));

    function addActivity() {
      console.log('indexColorDraw', indexColorDraw);
      if (drawMode.status) {
        userClick.value = true;
        return idColor.value = Number(indexColorDraw.index);
      }

      if (colors.length === idColor.value + 1) {
        userClick.value = false;
        return idColor.value = 0;
      }

      userClick.value = true;
      idColor.value += 1;
    }

    const getColor = computed(() => colors[String(idColor.value)]);

    watch(clear, () => {
      idColor.value = 1;
    });

    watch(fill, () => {
      if (!userClick.value) idColor.value = Math.floor(Math.random() * (colors.length - 1));
    });

    function handleEvent() {
      if (drawMode.status) addActivity();
    }

    return {
      handleEvent,
      clear,
      colors,
      getColor,
      addActivity,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.day {
  background: rgba(27, 31, 35, .06);
  border-radius: 2px;
  color: #fff;
  cursor: pointer;
  display: block;
  height: 10px;
  margin: 1.5px;
  outline: 1px solid rgb(56 56 56 / 42%);
  outline-offset: -1px;
  width: 10px;
}
</style>
