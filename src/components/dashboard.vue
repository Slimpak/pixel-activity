<template>
  <div class="" >
    <YearItem
      v-for="year, index in 3"
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
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
