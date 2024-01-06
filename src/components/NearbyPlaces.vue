<!-- src/components/NearbyPlaces.vue -->
<template>
  <div>
    <h1>Nearby Places</h1>
    <form  class="form-container">
      <div class="form-group">
        <label for="longitude" class="label-group">Longitude:</label>
        <input type="text" class="input-group" v-model="longitude" required />
      </div>

      <div class="form-group">
        <label for="latitude" class="label-group">Latitude:</label>
        <input type="text" class="input-group" v-model="latitude" required />
      </div>

      <div class="form-group">
        <label for="radius" class="label-group">Radius:</label>
        <input type="text" class="input-group" v-model="radius" required />
      </div>

      <button type="submit" class="button">Get Nearby Places</button>
    </form>

  </div>
</template>
  
<script>
export default {
  data() {
    return {
      longitude: "",
      latitude: "",
      radius: "",
      places: [],
    };
  },
  methods: {

  },
};
</script>
  
<style scoped>

.form-container {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.button {
  background-color: #4caf50;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  height: 55px;
}

.button:hover {
  background-color: #45a049;
}
</style>