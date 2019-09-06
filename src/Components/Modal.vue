<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <h6 class="modal-title">Изменение информации о стране</h6>
          </div>

          <div class="modal-body">
            <div class="container">
              <div class="row">
                <div class="col">
                  <input v-model="formData.name" type="text" class="form-control" placeholder="Наименование страны">
                  <small v-if="formData.name == '' || emptyName" class="form-text text-muted">Поле обязательно для заполнения</small>
                </div>
              </div>
              <div class="row">
                <div class="col">
                  <input v-model="formData.capital" type="text" class="form-control" placeholder="Столица">
                </div>
              </div>
              <div class="row">
                <div class="col">
                  <input v-model="formData.region" type="text" class="form-control" placeholder="Регион">
                </div>
              </div>
              <div class="row">
                <div class="col">
                  <input v-model="formData.population" type="number" class="form-control" placeholder="Население">
                </div>
              </div>
              <div class="row">
                <div class="col">
                  <button :disabled="formData.name === ''" class="btn btn-block btn-primary save-btn
" @click="$emit('save', formData)">
                    Сохранить
                  </button>
                </div>
                <div class="col">
                  <button class="btn btn-block btn-outline-secondary close-btn" @click="$emit('close')">
                    Отмена
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
    export default {
        name: "Modal",
        data () {
            return {
                emptyName: false,
                formData: {
                    name: '',
                    capital: '',
                    region: '',
                    population: ''
                }
            }
        },
    }
</script>

<style scoped>
  .row {
    margin: 20px 0;
  }

  .modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .5);
    display: table;
    transition: opacity .3s ease;
  }

  .modal-wrapper {
    display: table-cell;
    vertical-align: middle;
  }

  .modal-container {
    width: 35%;
    margin: 0 auto;
    background-color: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
    transition: all .3s ease;
    font-family: Helvetica, Arial, sans-serif;
  }

  .modal-header {
    background-color: rgba(0, 0, 0, .05);
  }

  .modal-header h3 {
    margin-top: 0;
    color: #42b983;
  }

  .modal-body {
    text-align: left;
    margin: 20px 40px;
    padding-left: 0;
    padding-right: 0;
    padding-bottom: 36px;
  }

  .modal-enter {
    opacity: 0;
  }

  .modal-leave-active {
    opacity: 0;
  }

  .modal-enter .modal-container,
  .modal-leave-active .modal-container {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
</style>
