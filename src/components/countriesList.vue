<template>
  <div> 
      <p @click="getDetails(name)">{{country}}</p>
  </div>
</template>

<script>
export default {
name:"CountriesList",
props:[
    "country",
    "getDetails",
    "name"
]
}
</script>

<style>

</style>