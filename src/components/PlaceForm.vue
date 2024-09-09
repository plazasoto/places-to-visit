<template>
    <div>
        <label for="place-select">Selecciona un lugar</label>
        <select v-model="selectedPlace" id="place-select">
            <option value="" disabled selected>Selecciona un lugar</option>
            <option v-for="place in places" :key="place.cca3" :value="place.name.common">
              {{ place.name.common }}
            </option>
        </select>
        <button @click="addPlace">Añadir un lugar</button>

        <p v-if="errorMessage" style="color: red">{{ errorMessage }}</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  
  export default {
    data(){
      return{
        places: [],
        selectedPlace: null,
        errorMessage:"",
      }
    },
    methods:{
      fetchPlaces(){
        axios.get('https://restcountries.com/v3.1/all').then(response => {
          this.places = response.data;
        });
      },
  
      addPlace(){
        if(!this.selectedPlace){
            this.errorMessage = "Por favor selecciona un lugar antes de añadirlo.";
        }else{
            this.$emit('addPlace', this.selectedPlace);
            this.errorMessage = "";
        }

      },
    },
    mounted(){
      this.fetchPlaces();
    },
  }
  </script>
  
  <style>
    
  </style>