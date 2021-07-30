<template>
<div>
    <AutoComplete
      placeholder="search countries"
      @on-search="handleSearch"
      style="width:200px"
      icon="ios-search"
      @on-clear="clearSearch"
      clearable
    >
    </AutoComplete> <br> <br>

    <Row type="flex" >
      <country-details
        v-for="(country,index) in countries"
        :country="country"
        :key="index"
      ></country-details>
    </Row>
</div>

</template>

<script>
import CountryDetails from '../components/CountryDetails.vue'
import axios from 'axios'
export default {
  data() {
    return {
      allCountries: null,
      countries: null,
    };
  },
  components: {
    CountryDetails,
  },
  methods:{
    async init(){
      var countries = await axios
        .get("https://restcountries.eu/rest/v2/all")
        .then((response) => (this.countries = response["data"]))
        .catch((error) => window.alert("country data fetch: " + error));
      this.allCountries = countries.map(x => {return {name : x.name, region: x.region, languages: x.languages, capital: x.capital, flag: x.flag }});
      this.countries = [...this.allCountries]
    },
    
    clearSearch(){
      this.countries = [...this.allCountries]
    },

    
    handleSearch(value){
        this.countries = []
        this.allCountries.forEach(country => {
           if(country.name.toLowerCase().indexOf(value.toLowerCase()) !== -1)
            this.countries.push(country)
        });

    }
  },
  created() {
    this.init()
  }
}

</script>