<template>
    <div
      class="day"
      :style="`background: ${ getColor };`"
      @click="addActivity()"
      @mouseover='handleEvent'
    >
      
    </div>
  </template>
  
  <script>
  import { ref, computed, inject, watch } from 'vue';

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
          return idColor.value = Number(indexColorDraw.index)
        }

        if (colors.length === idColor.value + 1) {
          userClick.value = false;
          return idColor.value = 0;
        }

        userClick.value = true;
        idColor.value += 1;
      }

      const getColor = computed(() => {
        return colors[String(idColor.value)] 
      });

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
        addActivity
      };
  },
    props: {
      msg: String
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  .day {
    cursor: pointer;
    color: #fff;
    display: block;
    width: 10px;
    height: 10px;
    background: rgba(27, 31, 35, 0.06);
    outline: 1px solid rgb(56 56 56 / 42%);
    outline-offset: -1px;
    border-radius: 2px;
  }
  </style>
  