<template>
    <div class="col-md-12 text-center">
        <h3>Gallery</h3>
        <div class="gallery">
            <img v-if="selectedPhoto == ''" v-bind:src="mainimg" alt="" width="400px" id="mainPhoto">
            <img v-else v-bind:src="selectedPhoto" alt="" width="400px" id="mainPhoto">
            <ul class="list-inline gallery">
                <li class="list-inline-item" v-for="(img,index) in pictures"  v-bind:key="index">
                    <img v-bind:src="img.thumbnail" alt="" width="40px" v-bind:linkto="img.photo" v-on:click="getPhoto($event)">
                </li>
            </ul>
        </div>
    </div>
</template>
<script>

export default {
    props:["pictures","mainimg"],
    watch:{
        pictures: function(newVal){
            this.pictures = newVal,
            this.selectedPhoto = newVal[0].photo;
        }
    },
    name: 'Gallery',

  data(){
    return {
    selectedPhoto: "" 
    }
  },
  methods:{
      getPhoto: function($event){
          //console.log(event.srcElement.attributes[3].nodeValue);
          this.selectedPhoto = $event.srcElement.attributes[3].nodeValue;
      }
      
  }

  
}
</script>
<style>
    ul.gallery {
    max-width: 400px;
    overflow-x: scroll;
    display: flex;
        margin: 15px auto;
}
</style>