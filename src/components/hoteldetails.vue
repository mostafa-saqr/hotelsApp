<template>
    <div class="container">
        <div class="card">
            <div class="row">
                <div class="card-body">
                    <div class="col-md-12">
                        <h1>{{hotelName}}</h1>
                    </div>
                    <div class="col-md-3">
                        <p> Choose no of nights : {{noOfNigths}} </p>
                        <div class="input-group mb-3">
                            <select class="custom-select" id="noOfNights" v-on:change="changeNigths($event)">
                                <option value="1" selected>One</option>
                                <option value="2">Two</option>
                                <option value="3">Three</option>
                            </select>
                        </div>
                    </div>
                    <Gallery v-bind:pictures="gallery" v-bind:mainimg="mainimg"/>
                    <Reviews v-bind:reviews="reviews"/>
                </div>
            </div>
        </div>
        
    </div>
</template>
<script>
import Gallery from './hoteldetails/gallery.vue';
import Reviews from './hoteldetails/reviews.vue';
const axios = require('axios');
export default {
    name: 'HotelDetails',
      components: {
        Gallery,
        Reviews
    },
    props:['noOfNigths',"hotelID"],
    watch:{
        hotelID: function(newVal){
             this.getHotelsDetails(newVal)
        }
    },
  data(){
    return {
        noNigths:this.noOfNigths,
        hotelName:"",
        gallery:"",
        mainimg:"",
        reviews:""
    }
  },
  methods:{
     
      getHotelsDetails: function(hotel){
         
          var that = this;
          axios.get(`http://my-json-server.typicode.com/fly365com/code-challenge/hotelDetails/${hotel}`).then((response) => {
          that.hotelName = response.data.name,
          that.gallery = response.data.pictures,
          that.reviews = response.data.reviews,
          that.mainimg = response.data.pictures[0].photo
          })
      },
      changeNigths: function($event){
          this.noNigths = Number($event.srcElement.value);
          this.$emit('changeNights', this.noNigths)
       
      }
  },
  mounted(){
      this.getHotelsDetails(this.hotelID)
  },
  
}
</script>