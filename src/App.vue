<template>
  <div>
    <input v-model="filter" placeholder="Filter by name" />
    <crime-statistics :localities="localityData" :filter="filterLocality" />
  </div>
</template>

<script>
import CrimeStatistics from '@/components/CrimeStatistics.vue';
import localityData from "@/data/localityData.json";

export default {
  name: 'App',
  components: {
    CrimeStatistics
  },
  data() {
    return {
      localityData,
      filter: ""
    };
  },
  computed: {
    filterLocality() {
      return this.filter;
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
