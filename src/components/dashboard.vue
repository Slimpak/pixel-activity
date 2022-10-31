<template>
  <div class="" >
    <YearItem
      v-for="year, index in countYears"
      :key="index"
      :top-year="index == 0"
    >
    </YearItem>
  </div>
</template>

<script>
import YearItem from './YearItem.vue'

export default {
  name: 'dashBoard',
  components: {
    YearItem,
  },
  props: {
      countYears: {
          type: Number,
          default: 0,
      },
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
