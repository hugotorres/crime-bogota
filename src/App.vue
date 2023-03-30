<template>
  <div>
    <select v-model="city">
      <option disabled value="">Please select one</option>
      <option value="bogota">Bogotà</option>
      <option value="medellin">Medellin</option>
    </select>
    <input v-model="filter" placeholder="Filter by name" />
    <crime-statistics :localities="computedCity" :filter="filterLocality" />
  </div>
</template>

<script>
import CrimeStatistics from '@/components/CrimeStatistics.vue';
import localityData from "@/data/localityData.json";
import medellin from "@/data/medellin.json";

export default {
  name: 'App',
  components: {
    CrimeStatistics
  },
  data() {
    return {
      city: "bogota",
      localityData,
      medellin,
      filter: ""
    };
  },
  computed: {
    computedCity() {
      return this.city === "bogota" ? this.localityData : this.medellin;
    },
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
