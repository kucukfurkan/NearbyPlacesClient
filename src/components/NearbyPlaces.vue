<!-- src/components/NearbyPlaces.vue -->
<template>
  <div class="nearby-places">
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

      <button type="submit" class="button">Nearby Places</button>
    </form>
  </div>
  <div></div>
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
    async getNearbyPlaces() {
      try {
        const response = await this.$axios.get('http://localhost:8070/api/places', {
          params: {
            longitude: this.longitude,
            latitude: this.latitude,
            radius: this.radius,
          },
        });

        this.places = response.data;
      } catch (error) {
        console.error('Error fetching nearby places:', error);
      }
    },
  },
};
</script>
  
<style scoped>
.form-container {
    min-height: 100vh; 
    display: flex;
    flex-direction: row;
    max-width: 600px; 
    margin: 0 auto; 
    padding: 20px;
    align-items: flex-start;
  }

  .nearby-places{
    padding-top: 0px;
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
    margin-right:24px;
  }

  .button {
    background-color: #4caf50;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
    width:70px;
    height: 50px;
    margin-top: 20px;
  }

  @media (min-width: 600px) {
    .form-container {
      max-width: 600px; 
    }

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