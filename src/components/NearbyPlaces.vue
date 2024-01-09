<!-- src/components/NearbyPlaces.vue -->
<template>
  <div class="outerdiv">
    <div>
      <h1>Nearby Places</h1>
      <form @submit.prevent="getNearbyPlaces" class="form-container">
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
    <div class="result-container">
      <div v-if="places.length > 0">
        <h2>Places:</h2>
        <ul>
          <li v-for="(place, index) in places" :key="index">
            <strong>{{ place.placeName }}</strong>
            <p>{{ place.address || 'Address not available' }}</p>
          </li>
        </ul>

        <div v-if="error">
          <p>Error fetching nearby places: {{ error }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
  
<script>
import axios from 'axios';
export default {
  data() {
    return {
      longitude: "",
      latitude: "",
      radius: "",
      places: [],
      error: null,
    };
  },
  methods: {
    async getNearbyPlaces() {
      try {
        const axiosInstance = axios.create({
          baseURL: 'http://localhost:8070/api', // Adjust the base URL as needed
        });
        const response = await axiosInstance.get('http://localhost:8070/api/places/nearby', {
          params: {
            longitude: this.longitude,
            latitude: this.latitude,
            radius: this.radius,
          },
        });

        this.places = response.data;
        console.log(this.places)
        this.error = null;
      } catch (error) {
        console.error('Error fetching nearby places:', error);
        this.error = 'An error occurred while fetching nearby places.';
      }
    },
  },
};
</script>
  
<style scoped>
.outerdiv {
  display: flex;
  flex-direction: column;
}

.form-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  display: flex;
  flex-direction: row;
}

.result-container {
  max-width: 600px;
  margin: 20px auto;
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 15px;
  align-items: flex-start;
}

.label-group {
  display: block;
  margin-bottom: 5px;
}

.input-group {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
  margin-right: 24px;
}

.button {
  background-color: #4caf50;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
  width: 100%; /* Full width button */
  margin-top: 20px;
}

@media (min-width: 600px) {
  .form-group {
    flex-direction: row;
    align-items: center;
  }

  .label-group {
    margin-right: 10px;
  }

  .input-group {
    width: 150px;
  }
}
</style>