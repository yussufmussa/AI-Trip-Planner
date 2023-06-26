<template>
  <div class="container mx-auto">
    <div class="max-w-md mx-auto mt-8">
      <div class="bg-white rounded-lg shadow-lg p-6">
        <h1 class="text-2xl font-bold mb-4">Trip Planner</h1>
        <h2 class="text-lg text-gray-600 mb-4">Plan your trip</h2>

        <div class="flex items-center mb-4">
          <input v-model="location" type="text" id="location" class="rounded-full border-gray-300 py-2 px-4 w-full"
            placeholder="Enter location" />
        </div>

        <div class="flex items-center mb-4">
          <input v-model="days" type="text" id="days" class="rounded-full border-gray-300 py-2 px-4 w-full"
            placeholder="Enter number of days" />
        </div>

        <button @click="getTripPlan"
          class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-full w-full">
          <span v-if="loading">Loading...</span>
          <span v-else>Plan Trip</span>
        </button>

      </div>
      <div v-if="error" class="mt-4 text-red-500">{{ error }}</div>
    </div>
  </div>
  <!--  Dispay itenary-->
  <div class="container mx-auto">
    <div v-if="tripPlan" class="bg-gray-100 p-4 rounded">
    <h2 class="text-lg font-bold mb-2">Trip Plan for {{ location }}</h2>
    <div v-for="day in tripPlan.plan" :key="day.day" class="mb-4">
      <h3 class="text-md font-bold mb-2">Day {{ day.day }}</h3>
      <ul>
        <li v-for="activity in day.activities" :key="activity.description" class="ml-4">
          <span class="font-bold">{{ activity.time }}</span> - {{ activity.description }}
        </li>
      </ul>
    </div>
  </div>
  </div>
  
  <!--  end itinery display -->
</template>

  
<script>
import axios from 'axios';

export default {
  data() {
    return {
      location: '',
      tripPlan: '',
      loading: false,
      error: '', // Add the 'error' property to store the error message
    };
  },
  methods: {
    async getTripPlan() {
      if (this.location === '') {
        this.error = 'Location cannot be empty';
      } else if (this.days === '') {
        this.error = 'Days cannot be empty';
      } else {
        const options = {
          method: 'GET',
          url: 'https://ai-trip-planner.p.rapidapi.com/',
          params: {
            days: this.days,
            destination: this.location
          },
          headers: {
            'X-RapidAPI-Key': '2efda3b728msh32adae685147d60p1e5ff5jsn03dabe02ac2f',
            'X-RapidAPI-Host': 'ai-trip-planner.p.rapidapi.com'
          }
        };

        this.error = '';
        this.loading = true;
        try {
          const response = await axios.request(options);
          this.tripPlan = response.data;
        } catch (error) {
          console.error(error);
        } finally {
          this.loading = false;
        }

      }
    },
  },
};
</script>
  
  