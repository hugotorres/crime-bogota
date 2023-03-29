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
    <template>
      <div>
        <label for="filter">Filter by Locality:</label>
        <input type="text" id="filter" v-model="filter">
        <div class="row header">
          <div class="cell">Locality</div>
          <div class="cell">Crime Rate</div>
          <div class="cell">Population</div>
          <div class="cell">Crime Rate per Person</div>
          <div class="cell">Area</div>
          <div class="cell">Number of Police Stations</div>
        </div>
        <div v-for="locality in filteredData" :key="locality.id" class="row">
          <div class="cell">{{ locality.name }}</div>
          <div class="cell">{{ locality.crimeRate }}</div>
          <div class="cell">{{ locality.population }}</div>
          <div class="cell">{{ locality.crimeRatePerPerson }}</div>
          <div class="cell">{{ locality.area }}</div>
          <div class="cell">{{ locality.numPoliceStations }}</div>
        </div>
      </div>
    </template>
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

.row {
  display: flex;
  flex-direction: row;
}

.cell {
  padding: 10px;
  margin: 5px;
  border: 1px solid black;
  flex: 1;
}

.header {
  font-weight: bold;
}
</style>