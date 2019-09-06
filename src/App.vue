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
    <div class="body-content">
      <cards v-bind:countries="countries" v-bind:state="state" v-if="this.state === 'cards'" @openModalWindow="openModalWindow"></cards>
      <modal v-if="showModal" @save="getFormData" @close="closeModalWindow"></modal>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    import Cards from './Components/Cards.vue'
    import Modal from './Components/Modal.vue'
    import Vue from 'vue'

export default {
    name: 'app',
    data () {
        return {
            countries: null,
            state: 'cards',
            showModal: false,
            targetCard: null,
            formData: null
        }
    },
    mounted() {
        axios
            .get('https://restcountries.eu/rest/v2/all?fields=name;capital;region;population;flag')
            .then(response => {
                this.countries = response.data;
                this.countries.sort(function (a, b) {
                    if(a.name.toUpperCase() < b.name.toUpperCase()) {
                        return -1;
                    }
                    if(a.name.toUpperCase() > b.name.toUpperCase()) {
                        return 1
                    }
                });
            });
    },
    methods: {
        openModalWindow: function(country) {
            this.targetCard = country;
            this.state = 'modal';
            this.showModal = true
        },
        getFormData: function(formData) {
            this.formData = formData;
            this.state = 'cards';
            this.showModal = false;
            this.changeNewCard();
        },
        changeNewCard: function() {
            Vue.set(this.countries, this.targetCard, {
                capital: this.checkValue('capital'),
                flag: this.countries[this.targetCard].flag,
                name: this.formData.name,
                population: Number(this.checkValue('population')),
                region: this.checkValue('region')
            })
        },
        checkValue: function(value) {
            if(this.formData[value] === '') {
                return this.countries[this.targetCard][value]
            } else {
                return this.formData[value]
            }
        },
        closeModalWindow: function () {
            this.state = 'cards';
            this.showModal = false;
            this.targetCard = null
        }
    },
    components: {
        Cards,
        Modal
    }
}
</script>

<style lang="scss">

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
</style>
