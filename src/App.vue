<template>
<body>
    <!-- Example of what could be rendered -->

    <div>
       <NavBar />
       <router-view />

        <!-- container wrapper div -->
        
    </div>
    
</body>

<!-- <NavBar /> -->


<!-- <CountriesList /> -->
<!-- con el router view ya muestro en el template el componente asociado a ese URL -->
<!-- <router-view /> -->
</template>
  
<script setup>

import NavBar from './components/NavBar.vue'
import CountriesList from './views/CountriesList.vue'
import CountryDetails from './views/CountryDetails.vue'
   
</script>
  
<style scoped>
  
</style>
