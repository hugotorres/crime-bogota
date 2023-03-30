<template>
  <div>
    <div class="switch-header">
      <label class="switch">
        <input type="checkbox" v-model="switchHeader">
        <span class="slider round"></span>
      </label>
    </div>
    <h2>Crime Statistics by Locality in Bogotá</h2>
    <table v-if="switchHeader">
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
    <div v-else>
      <label for="filter">Filter by Locality:</label>
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
    return {
      switchHeader: false
    }
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
.switch-header {
  float: left;
}

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

/* The switch - the box around the slider */
.switch {
  position: relative;
  display: inline-block;
  width: 42px;
  height: 16px;
}
  
/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 8px;
  width: 8px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked+.slider {
  background-color: #2196F3;
}

input:focus+.slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked+.slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>