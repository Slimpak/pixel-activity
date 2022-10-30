<template>
  <div class="grid" >
    <div
      class="row"
      v-for="row in 7"
      :key="row"
    >
      <DayItem
        v-for="item in 52"
        :key="item"
      />
    </div>
  </div>
</template>

<script>
import DayItem from './DayItem.vue'

export default {
  name: 'dashBoard',
  components: {
    DayItem,
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .grid {
    display: flex;
    align-items: center;
    flex-direction: column;
    gap: 3px;
  }

  .row {
    display: flex;
    gap: 3px;
  }

</style>
