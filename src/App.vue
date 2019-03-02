<template>
  <div id="app">
    <h2>Days until End of CAT:</h2>
    <p class="time">
      <span>days: {{days}},&nbsp;</span>
      <span>hours: {{hours}}, &nbsp;</span>
      <span>minutes: {{minutes}}, &nbsp;</span>
      <span>seconds: {{seconds}}&nbsp;</span>
    </p>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      days: 0,
      hours: 0,
      minutes: 0,
      seconds: 0
    }
  },
  beforeCreate: function() {
    window.setInterval(() => {
      const future = new Date(2019, 6, 16).getTime();
      const now = new Date().getTime();

      let delta = Math.abs(future - now) / 1000;

      // calculate (and subtract) whole days
      this.days = Math.floor(delta / 86400);
      delta -= this.days * 86400;

      // calculate (and subtract) whole hours
      this.hours = Math.floor(delta / 3600) % 24;
      delta -= this.hours * 3600;

      // calculate (and subtract) whole minutes
      this.minutes = Math.floor(delta / 60) % 60;
      delta -= this.minutes * 60;

      // what's left is seconds
      this.seconds = Math.floor(delta % 60);
    }, 1000)
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Poppins');
#app {
  font-family: 'Poppins', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: #ff9350;
  padding: 100px 30px;
  height: 100vh;
}

h2 {
  margin-top: 0;
}

.time {
  display: flex;
  flex-direction: column;
  text-align: left;
  width: 38%;
  margin: 0 auto;
}

@media screen and (min-width: 600px) {
  .time {
    flex-direction: row;
    justify-content: center;
    width: 100%;
  }
}
</style>
