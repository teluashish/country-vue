<template>
        <Col :xs="24" :sm="24" :md="12" :lg="8" :xl="6">
            <Card id="countryCard">

                <img id="flag" :src="country.flag" height="200" width="300"  />

                 <br /><br />
                <div id="cardDetails">
                <p><b>Name: </b>{{country.name}}</p>
                <p><b>Continent: </b>{{country.region}}</p>
                <p><b>Languages: </b><span v-for="(language,index) in country.languages" :key="index">{{language.name}}<span v-if="index + 1 < country.languages.length">, </span></span>.</p>
                <p><b>Capital: </b>{{country.capital}}</p>
                </div>
            </Card>
        </Col>

</template>

<script>
export default {
    props:['country'],
}
</script>

<style scoped>
img {
  border-radius: 2%;
}
#cardDetails{
    text-align: left;
}
#countryCard{
    width:350px;
    margin: 10px;
}

#flag{
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 98%;
}

</style>
