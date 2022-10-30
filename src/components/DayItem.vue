<template>
    <div
      class="day"
      :style="`background: ${ getColor };`"
      @click="addActivity()"
    >
      
    </div>
  </template>
  
  <script>
  import { ref, computed, inject } from 'vue';

  export default {
    name: 'DayItem',
    setup() {
      const colors = inject('arrayColors', ref([]));
      const idColor = ref(Math.floor(Math.random() * colors.length));

      function addActivity() {
        if (colors.length === idColor.value) return idColor.value = 1;
        idColor.value += 1;
      }

      const getColor = computed(() => {
        return colors[String(idColor.value)] 
      });


      return {
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
  