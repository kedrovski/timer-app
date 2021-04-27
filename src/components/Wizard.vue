<template>
    <div>
    			<hr/>
          <label>Enter the number of seconds:</label><br>
          <input type="number" v-model="secQuantity" placeholder="seconds">
          <button @click="runTimer" v-if="isBtnAvailable()">
            Run timer
          </button>
          <button @click="stopTimer" v-if="!isBtnAvailable()">
            Stop timer
          </button>
          <Timer :counter="counter" class="timer"></Timer>
          <p>{{currentTime | date}}</p>
          <hr/>
    </div>
</template>

<script>
import Timer from '../components/Timer.vue';
import { interval } from 'rxjs';

export default {
  name: 'Wizard',
  props: {
    msg: String
  },
  components: {
    Timer
  },
  mounted() {
    this.intervalSource = interval(10);
  },
  filters: {
    date: function(str) {
      if (!str) { return '-'; }
      const index = str.indexOf('T');
      return `${str.slice(0, index)} ${str.slice(index+1).replace('Z','')}`;
    }
  },
  data: function() {
    return { 
      secQuantity: 10, 
      counter: 0, 
      timeoutId: null, 
      currentTime: null,
      intervalSubscribe: null,
      intervalSource: null
    }
  },
  methods: {
    runTimer: function () {
      if (!this.intervalSubscribe) {
        let milliSec = this.secQuantity * 1000;
        this.counter = milliSec;
        this.currentTime = null;
        let timeBefore = new Date().getTime();

        this.intervalSubscribe = this.intervalSource.subscribe(value => {
          let timeNow = new Date().getTime();
          let timeDiff = timeNow - timeBefore;
          this.counter = milliSec - timeDiff;
        });

        this.timeoutId = setTimeout(() => {
          this.stopTimer();
        }, milliSec);
      }
    },
    stopTimer: function () {
      if (this.timeoutId) {
        this.intervalSubscribe.unsubscribe();
        this.intervalSubscribe = null;
        clearTimeout(this.timeoutId);
        this.counter = 0;
        this.finishHandler();
      }
    },
    isBtnAvailable: function() {
     	return this.counter <= 0;
    },
    finishHandler: function() {
    	this.currentTime = new Date().toISOString();
    },
  }
}
</script>

<style scoped>
.timer {
  background-color: #2e71ff;
  height: 40px;
  width: 100px;
  color: #fff;
  text-align: center;
  line-height: 40px;
  border-radius: 10px;
  border: 2px solid #2e71ff;
  margin-top: 10px;
  font-size: 25px;
}
input {
  border-radius: 10px;
  outline: none;
  border: 2px solid #2e71ff;
  height: 22px;
  padding: 2px 10px;
}
.shadow-btn {
  box-shadow: 2px 5px 16px 0px #0B325E, 5px 5px 15px 5px rgba(0,0,0,0);
}
label {
  margin-bottom: 10px;
  color: #39464e;
  display: inline-block;
}
</style>
