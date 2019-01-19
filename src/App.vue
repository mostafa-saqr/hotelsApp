<template>
  <div id="app">
    
    <ListOfHotels  v-bind:hotels="hotels" v-bind:noOfNigths="noOfNigths"  v-on:getSelectedHotel="updateHotel($event)" v-bind:hotelID="hotelID"/>
    <hr>

    <HotelDetails v-if="hotelID !== '' " v-bind:noOfNigths="noOfNigths" v-on:changeNights="updateNoOfNights($event)" v-bind:hotelID="hotelID"/>
    

  </div>
</template>

<script>
const axios = require('axios');
import ListOfHotels from './components/listofhotels.vue';
import HotelDetails from './components/hoteldetails.vue';


export default {
  name: 'app',
  components: {
    ListOfHotels,
    HotelDetails
  },
  data(){
    return {
      noOfNigths:1,
      hotels:[],
      hotelID:""
    }
  },
  methods: {
    getHotels: function(){
        var that = this;
        axios.get('http://my-json-server.typicode.com/fly365com/code-challenge/hotels').then(response => (
        that.hotels = response.data,
        that.hotelID = response.data[0].id
        //console.log(that.hotelID)
        ))
      },
    updateNoOfNights:function(night){
      this.noOfNigths = night
    },
    updateHotel:function(hotel){
      this.hotelID = hotel;
      //console.log(this.hotelID)
    }
  },
  mounted(){
    this.getHotels()
  }
}
</script>

<style>
body{
      background-color: #f5f2ef;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  margin-top: 60px;
}

</style>
