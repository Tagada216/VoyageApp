<template>
  <div id="app">
    <p>Voyage </p>
    <div>
      <p>
        Rechercher : <input v-model="country">
      </p>
      <button @click="getOneCountry(country)">Rechercher</button>
    </div>
    <div v-for="country in listCountries " :key="country.name">
      <countries-list :country="country.translations.fr" :getDetails="getDetails" :name="country.name"></countries-list>
    </div>
<modal name="detail-modal">
    <div v-if="oneCountry">
      <p>
        Pays : {{oneCountry.translations.fr}}
      </p>
      <br>
      <p>
        Capitale : {{oneCountry.capital}}
      </p>
    </div>
</modal>
<modal name="one-modal">
    <div v-if="oneCountry">
      <p>
        Pays : {{oneCountry.translations.fr}}
      </p>
      <br>
      <p>
        Capitale : {{oneCountry.capital}}
      </p>
    </div>
</modal>
  </div>
</template>

<script>
import CountriesList from './components/countriesList.vue'
import axios from "axios";
export default {
  name: 'App',
  components: {
    CountriesList
  },
  data(){
    return{
      listCountries: null,
      oneCountry: null
    }
  },
  mounted(){
    this.getAllCoutries()
    console.log("tab", this.listCountries)
  },
  methods:{
    getAllCoutries(){
      axios.get("https://restcountries.eu/rest/v2/all").then(resp =>{
        this.listCountries = resp.data
      }).catch(error => console.log(error))
    },
    getDetails(name){
      this.$modal.show('detail-modal');
      axios.get(`https://restcountries.eu/rest/v2/name/${name}?fullText=true`).then(resp =>{
        this.oneCountry = resp.data[0]
      }).catch(error => console.log(error))     
    },
    getOneCountry(name){
       this.$modal.show('detail-modal');
        axios.get(`https://restcountries.eu/rest/v2/name/${name}`).then(resp =>{
        this.oneCountry = resp.data[0]
      }).catch(error => console.log(error))   
    }
  }
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
