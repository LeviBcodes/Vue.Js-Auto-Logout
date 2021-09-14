<template>
  <div>
    Hello
  </div>
</template>

<script>
export default {
  name: 'AutoLogout',
  data: function () {
    return{
      //events or iput to listen for from the user
      events: ['click', 'mousemove', 'mousedown', 'scroll', 'keypress', 'load'],
      warningTimer: null,
      logoutTimer: null,
    }
  },
  unmounted() {
    this.events.forEach((event) => {
      window.removeEventListener(event, this.resetTimer)
    });
    this.resetTimers();
  },
  mounted() {
    //listen for any events from the user
    this.events.forEach((event) => {
      window.addEventListener(event, this.resetTimer)
    });
    this.setTimers();
  },
  methods: {
    setTimers: function() {
      //this method will invoke the warningMessage method giving the user feedback, warning them they are about to be logged out if they are inactive
      this.warningTimer = setTimeout(this.warningMessage, 14 * 60 * 1000);
      this.logoutTimer = setTimeout(this.warningMessage, 15 * 60 * 1000);
    },
    warningMessage: function () {
      //this is the warning message
      alert('warning');
    },
    logoutUser: function () {
      //this method will logout the user. adjust to fit your application
      document.getElementById('logout-form').submit;
    },
    resetTimer: function () {
      //if any input is detected the warningTimer method will be reset, keeping the user signed in
      clearTimeout(this.warningTimer);
      clearTimeout(this.logoutTimer);
      this.setTimers();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
</style>
