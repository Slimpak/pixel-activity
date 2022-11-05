<template>
  <div>
    <YearItem
      v-for="year, index in countYears"
      :key="index"
      :top-year="index == 0"
    />
  </div>
</template>

<script>
import YearItem from './YearItem.vue';

export default {
  name: 'DashBoard',
  components: {
    YearItem,
  },
  props: {
    countYears: {
      type: Number,
      default: 0,
    },
  },
};
</script>
