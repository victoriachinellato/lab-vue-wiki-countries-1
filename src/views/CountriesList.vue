<template>

<div class="column is-4" style="overflow: auto">
<div v-for="country in countries" >
<!-- <router-link> -->
    <div>
        <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="flag"/>
        <h1>{{country.name.common}}</h1>
    </div>
<!-- </router-link> -->
</div> 
</div>


                        
</template>
<script setup>
import countries from '../assets/countries.json' 
</script>
<style scoped>
</style>