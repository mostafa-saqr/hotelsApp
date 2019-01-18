<template>
    <div class="col-md-12">
        <h3>Reviews</h3>
        <a href="#/" v-on:click="sortUpReviews()"> sort Up</a> | 
        <a href="#/" v-on:click="sortDownReviews()"> sort Down</a>
        <ul class="list-unstyled">
            <span v-if="reviews == undefined ">Loading</span>
            <li v-else v-for="(comment,index) in reviews.slice(paginationFrom, paginationFrom + 3)" v-bind:key="index">
                <strong> {{index + 1}} </strong>{{comment.score}} {{comment.review}}
            </li>
        </ul>
        <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li class="page-item"><a class="page-link" href="#/" v-on:click="backPagination()"> Previous </a></li>
                <span v-if="reviews == undefined ">Loading</span>
                <li class="page-item" v-else v-for="(pagination,index) in Math.ceil(reviews.length/3)" v-bind:key="index" v-on:click="getReviews($event)"> <a class="page-link" href="#/" v-bind:id="index"> {{index +1}}</a></li>
            </ul>
        </nav>
    </div>
</template>
<script>

export default {
    props:["reviews"],
    name: 'Reviews',
  data(){
    return {
    paginationFrom:0
    }
  },
  methods:{
      getReviews: function($event){
          this.paginationFrom = ($event.srcElement.innerText - 1) * 3;
      },
      backPagination:function(){
          if(this.paginationFrom !== 0){
              this.paginationFrom = this.paginationFrom - 3;
          }
      },
      sortUpReviews(){
          this.reviews.sort((a, b) => a.score > b.score ? 1 : -1 )
      },
      sortDownReviews(){
          this.reviews.sort((a, b) => a.score < b.score ? 1 : -1 )
      }
  }
}
</script>