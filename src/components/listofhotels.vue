<template>
    <div class="container">
        <div class="row">
            
            <div class="col-md-4" v-for="hotel in hotels" v-bind:key="hotel.id">
                <div class="card text-left">
                    <div class="card-body">
                         <a href="#/" v-bind:id="hotel.id" v-on:click="getSelectedHotel($event)">{{hotel.name}}</a>  
                    <div class="media">
                        <img class="mr-4" v-bind:src="hotel.photo" alt="Generic placeholder image">
                        <div class="media-body ">
                           <p><span class="text-success">$</span> <strong>{{hotel.pricePerNight * noOfNigths}}</strong> for {{noOfNigths}}  
                              <span v-if="noOfNigths < 2">night</span> <span v-else>nights</span>
                            </p>
                           <p>
                               {{hotel.totalScore}}
                                <span v-if="hotel.totalScore >= 9">Excellent</span>
                                <span v-if="hotel.totalScore < 9 && hotel.totalScore >= 8">Very Good</span>
                                <span v-if="hotel.totalScore <= 7">Good</span>
                           </p>
                           <p> {{hotel.totalReviews}} reviews</p>
                        </div>
                    </div>
                    </div>
                </div>
            </div>
           
           
        </div>
    </div>
</template>
<script>

export default {
    name: 'ListOfHotels',
    props:["noOfNigths","hotels","hotelID"],
    data(){
        return{
            selectedHotel:this.hotelID
        }
    },
    methods:{
        getSelectedHotel: function($event){
            this.selectedHotel = Number($event.srcElement.id);
            this.$emit('getSelectedHotel', this.selectedHotel);
            //console.log(this.selectedHotel)
        }
    }
}
</script>
<style  scoped>
    .card-body{
            box-shadow: 2px 2px 13px 0px rgba(128, 128, 128, 0.26);
    }
    .card-body:hover{
            background: rgba(128, 128, 128, 0.11)
    }
</style>
