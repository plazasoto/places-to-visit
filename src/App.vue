<template>
  <div id="app">
    <h1>Lugares que quiero visitar</h1>
    <PlaceForm @add-place="handleAddPlace"/>
    <ul>
      <li v-for="place of placesToVisit" :key="place">
        {{ place }}
        <button @click="removePlace(place)">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script>
  import PlaceForm from './components/PlaceForm.vue';
  export default{
    components:{
      PlaceForm,
    },

    data(){
      return{
        placesToVisit: [],
      }
    },

    methods:{
      handleAddPlace(place){
        if (place && !this.placesToVisit.includes(place)){
          this.placesToVisit.push(place);
          this.savePlaces();
        }
      },

      removePlace(place){
        this.placesToVisit = this.placesToVisit.filter(p => p !== place);
        this.savePlaces();

      },

      savePlaces() {

localStorage.setItem('placesToVisit', JSON.stringify(this.placesToVisit));

},

loadPlaces() {

const savedPlaces = localStorage.getItem('placesToVisit');

if (savedPlaces) {

  this.placesToVisit = JSON.parse(savedPlaces);

}

},
    },
  }
</script>

<style>
</style>
