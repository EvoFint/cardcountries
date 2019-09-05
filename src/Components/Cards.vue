<template>
  <div class="container">
    <div class="card-deck">
      <div class="card card_height text-left " v-for="(country, index) in countries">
        <div class="img-container">
          <img :src="country.flag" alt="" class="card-img-top img">
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-10">
              <h5 class="card-title">{{country.name}}</h5>
            </div>
            <div class="col-2">
<!--              <button>-->
                <img src="../ico/edit.svg" alt="" style="height: 1.5rem" @click="$emit('openModalWindow', index)">
<!--              </button>-->

            </div>
          </div>
          <div class="row">
            <div class="col">
              <div class="row">
                <div class="col txt">Столица</div>
                <div class="col txt">{{country.capital}}</div>
              </div>
              <div class="row">
                <div class="col txt">Регион</div>
                <div class="col txt">{{country.region}}</div>
              </div>
              <div class="row">
                <div class="col txt">Население</div>
                <div class="col txt">{{country.population}}</div>
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
        name: "Cards",
        props: {
            countries: Array
        }
    }
</script>

<style scoped lang="scss">
  /*@import "bootstrap";*/
  @import "~bootstrap/scss/functions";
  @import "~bootstrap/scss/variables";
  @import "~bootstrap/scss/mixins";

  .card {
    box-shadow: 3px 3px 5px rgba(0, 0, 0, 0.25);
    margin-bottom: 10px;
  }
  .card-title {
    white-space:nowrap;
    overflow: hidden;
    text-overflow: ellipsis
  }
  .card {
    min-width: 20%;
    max-width: 25%;
    margin-bottom: 30px;
  }
  /*@media (min-width:768px) {*/
  /*  .card-deck > .card*/
  /*  {*/
  /*    width: 25%;*/
  /*    flex-wrap: wrap;*/
  /*    flex: initial;*/
  /*  }*/
  /*}*/
  .card-columns {
  @include media-breakpoint-only(lg) {
    column-count: 4;
  }
  @include media-breakpoint-only(xl) {
    column-count: 4;
  }
  }
  .txt {
    white-space:nowrap;
    overflow: hidden;
    text-overflow: ellipsis
  }
  .col {
    p {
      margin-bottom: 0;
    }
  }
  .img-container {
    width: 100%;
    height: 11rem;
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: 1 0;
    }
  }
</style>
