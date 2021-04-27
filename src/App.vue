<template>
  <div id="app">
    <b>Welcome to the timer app!</b><br><br>
    <button @click="addNewTimer()" class="shadow-btn">Add new timer + </button>
    <br><br>
    <Wizard v-for="(item, index) in timersQuantity" :key="index"></Wizard>
  </div>
</template>

<script>
import Wizard from './components/Wizard.vue';

export default {
  name: 'App',
  components: {
    Wizard
  },
  data: function() {
        return { timersQuantity: [] }
  },
  methods: {
    addNewTimer: function () {
      this.timersQuantity.push('');
    }
  }
}
</script>

<style>
button {
    border-radius: 10px;
    border: 2px solid #ff4d4d;
    background-color: #fff;
    height: 30px;
    color: #ff4d4d;
    font-weight: 400;
    text-align: center;
    padding-left: 10px;
    padding-right: 10px;
    cursor: pointer; 
    margin-left: 10px;
}
button:active {
  box-shadow: none;
  outline: 0;
}
button:focus {
  outline: 0;
}
</style>
