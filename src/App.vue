<template>
  <div id="app">
    <div class="top-lane">
      <div class="container">
        <div class="row">
          <div class="col-10">
            <h1 class="h1_title">Страны мира</h1>
          </div>
          <div class="col-2">

          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="card-columns">
        <div class="card card_height text-left" v-for="country in countries">
          <div class="img-container">
            <img :src="country.flag" alt="" class="card-img-top img">
          </div>
          <div class="card-body">
            <div class="row">
              <div class="col-10">
                <h5 class="card-title">{{country.name}}</h5>
              </div>
              <div class="col-2">
                <img src="./ico/edit.svg" alt="" style="height: 1.5rem">
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
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'app',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
          countries: null
      }
    },
    mounted() {
          axios
              .get('https://restcountries.eu/rest/v2/all?fields=name;capital;region;population;flag')
              .then(response => (this.countries = response.data));
    },
    // filters: {
    //     limitName: function (value) {
    //         if(value > 15 )
    //
    //     }
    // }
}
</script>

<style lang="scss">
  @import "~bootstrap/scss/functions";
  @import "~bootstrap/scss/variables";
  @import "~bootstrap/scss/mixins";

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  margin-top: 0;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.h1_title {
  text-align: left;
}
.top-lane {
  width: 100%;
  height: 5%;
  border: 0.1px solid black;
  margin-bottom: 40px;
  background-color: #fff;
  box-shadow: 0 0 5px rgba(0,0,0,0.5);
}
.txt {
  white-space:nowrap;
  overflow: hidden;
  text-overflow: ellipsis
}
.card {
  box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
  margin-bottom: 10px;
}
.card-title {
  white-space:nowrap;
  overflow: hidden;
  text-overflow: ellipsis
}
.card-columns {
   @include media-breakpoint-only(lg) {
     column-count: 4;
   }
   @include media-breakpoint-only(xl) {
     column-count: 4;
   }
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
