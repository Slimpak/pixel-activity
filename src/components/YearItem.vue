<template>
    <div
      class="year"
      :class="{'year--top': topYear}"
    >
      <div class="year__days">
        <div v-for="title in ['Mon', 'Wed', 'Fri']" :key="title">
          {{ title }}
        </div>
      </div>
      <div class="year__mount" v-show="topYear">
        <div v-for="title in ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']" :key="title">
          {{ title }}
        </div>
      </div>
      <div class="year__title">
        <input type="text" value="2022">
      </div>
      <div
        class="row"
        v-for="row in 7"
        :key="row"
      >
        <DayItem
          v-for="item in 51"
          :key="item"
        />
      </div>
    </div>
  </template>
  
  <script>
  import DayItem from './DayItem.vue'
  
  export default {
    name: 'YearItem',
    components: {
      DayItem,
    },
    props: {
      topYear: {
          type: Boolean,
          default: true,
      },
    },
  }
  </script>
  
  <style lang="scss">
    .year {
      align-items: center;
      display: flex;
      flex-direction: column;
      margin-right: 20px;
      padding-left: 30px;
      position: relative;

      &--top {
        margin-top: 23px !important;
      }

      &__days {
        align-items: center;
        display: flex;
        flex-direction: column;
        height: 100%;
        justify-content: space-evenly;
        left: 0;
        position: absolute;
      }

      &__mount {
        align-items: baseline;
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        position: absolute;
        top: -20px;
        width: 100%;
      }

      &__title {
        align-items: baseline;
        display: flex;
        flex-direction: row;
        font-size: 14px;
        height: 20%;
        position: absolute;
        right: -26px;
        top: 33px;
        transform: rotate(90deg);

        input {
          background: transparent;
          border: 0;
          color: #fff;
          opacity: 0.5;
          width: 34px;
        }
      }
    }



  
    .row {
      display: flex;
      // gap: 3px;
    }
  
  </style>
  