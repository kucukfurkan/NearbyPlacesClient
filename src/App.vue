<template>
   <div id="app">
    
    <NearbyPlaces />
    
  </div>
</template>

<script >
import NearbyPlaces from "./components/NearbyPlaces.vue";

export default {
  name: 'App',
  components: {
    NearbyPlaces,
  },
};

</script>

<style scoped>

</style>
