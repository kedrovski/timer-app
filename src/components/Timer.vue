<template>
  <div> {{ formatTime(counter) }} </div>
</template>

<script>
export default {
  name: 'Timer',
  props: { 
    counter: { type: Number, required: true }
  },
  methods: {
    formatTime: function (milli) {
      let milliseconds = milli % 1000;
      let seconds = Math.floor((milli / 1000) % 60);
      seconds = seconds < 10 ? `0${seconds}` : seconds;
      if (String(milliseconds).length === 1) {
        milliseconds = `00${milliseconds}`;
      } else if (String(milliseconds).length === 2) {
        milliseconds = `0${milliseconds}`;
      }
      return `${seconds}:${milliseconds}`;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
