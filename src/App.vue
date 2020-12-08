<template>
  <div id="app">
    <progressiveTabs
      v-model="tabIndex" 
      :tabs="tabs"/>
    <div 
      v-if="selectedCountryID === null"
      class="item-container">
      <span 
        v-for="country in countries" 
        :key="country.id"
        class="item"
        @click="selectedCountryID = country.id; tabIndex++;">
        {{country.name}}
      </span>
    </div>
    <div 
      v-else-if="selectedCityID === null"
      class="item-container">
      <span
        v-for="city in citiesOfSelectedCountry"
        :key="city.id"
        class="item"
        @click="selectedCityID = city.id; tabIndex++;">
        {{city.name}}
      </span>
    </div>
    <div 
      v-else
      class="item-container">
      <span
        v-for="town in townsOfSelectedCity"
        :key="town.id"
        class="item"
        @click="selectedTownID = town.id; tabIndex++;">
        {{town.name}}
      </span>
    </div>
  </div>
</template>

<script>
import progressiveTabs from './progressiveTabs'
export default {
  name: 'App',
  components: {
    progressiveTabs
  },
  computed: {
    citiesOfSelectedCountry() {
      return this.cities.filter(el => el.countryID === this.selectedCountryID)
    },
    townsOfSelectedCity() {
      return this.towns.filter(el => el.cityID === this.selectedCityID)
    }
  },
  watch: {
    tabIndex(val) {
      if(val === 0) {
        this.selectedCountryID = null
        this.selectedCityID = null
        this.selectedTownID = null
      } else if(val === 1) {
        this.selectedCityID = null
        this.selectedTownID = null
      } else if(val === 2) {
        this.selectedTownID = null
      }
    }
  },
  data() {
    return {
      tabs: ['Countries', 'Cities', 'Towns'],
      tabIndex: 0,
      countries: [
        {id: 0, name: 'Turkey'},
        {id: 1, name: 'USA'},
        {id: 2, name: 'Russia'}
      ],
      cities: [
        {id: 0, countryID: 0, name: 'İstanbul' },
        {id: 1, countryID: 0, name: 'Sakarya'},
        {id: 2, countryID: 1, name: 'New York'},
        {id: 3, countryID: 1, name: 'San Francisco'},
        {id: 4, countryID: 2, name: 'Moscow'}
      ],
      towns: [
        {id: 0, cityID: 0, name: 'Taksim'},
        {id: 1, cityID: 1, name: 'Arifiye'},
        {id: 2, cityID: 2, name: 'Albion'},
        {id: 3, cityID: 3, name: 'Alameda'},
        {id: 4, cityID: 4, name: 'Dedovsk'},
      ],
      selectedCountryID: null,
      selectedTownID: null,
      selectedCityID: null
    }
  }
}
</script>

<style scoped>
.item-container {
  display: flex;
  flex-direction: column;
}
.item {
  background: gray;
  padding: 5px;
  width: 200px;
  margin-top: 10px;
  cursor: pointer;
  color: white;
}
</style>