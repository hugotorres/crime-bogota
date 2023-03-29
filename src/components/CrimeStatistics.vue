<template>
  <div>
    <h2>Crime Statistics by Locality in Bogotá</h2>
    <table>
      <thead>
        <tr>
          <th>Locality</th>
          <th>Population (2021)</th>
          <th>Reported Crimes (2020)</th>
          <th>Crime Rate (per 100,000 people)</th>
          <th>Crime Rate per Person</th>
          <th>Area (km²)</th>
          <th>Number of Police Stations</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="locality in filteredData" :key="locality.id">
          <td>{{ locality.name }}</td>
          <td>{{ locality.population }}</td>
          <td>{{ locality.reportedCrimes }}</td>
          <td>{{ locality.crimeRate }}</td>
          <td>{{ locality.crimeRatePerPerson }}</td>
          <td>{{ locality.area }}</td>
          <td>{{ locality.numPoliceStations }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "CrimeStatistics",
  props: {
    filter: String,
    localities: Array,
  },
  data() {
  },
  computed: {
    filteredData() {
      const regex = new RegExp(this.filter, "i");
      return this.localities.filter((locality) => regex.test(locality.name));
    },
  },
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th {
  background-color: #ddd;
}

th,
td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}
</style>