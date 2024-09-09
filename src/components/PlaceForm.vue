<template>
    <div>
        <label for="place-select">Selecciona un lugar</label>
<!--    <select v-model="selectedPlace" id="place-select">
            <option v-for="place in places" :key="place.cca3" :value="place.name.common">
                {{ place.name.common }}
            </option>
        </select> -->
        <select v-model="selectedPlace" id="place-select">
            <option v-for="place in places" :key="place.cca3" :value="place.name.common">
              {{ place.name.common }}
            </option>
        </select>
        <button @click="addPlaces">Añadir un lugar</button>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  
  export default {
    data(){
      return{
        places: [],
        selectedPlace: null,
      }
    },
    methods:{
      fetchPlaces(){
        axios.get('https://restcountries.com/v3.1/all').then(response => {
          this.places = response.data;
        });
      },
  
      addPlaces(){
        this.$emit('addPlace', this.selectedPlace);
      },
    },
    mounted(){
      this.fetchPlaces();
    },
  }
  </script>
  
  <style>
    
  </style>