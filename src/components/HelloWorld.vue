<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
      <div v-for="event in events">
        <h5>{{event.name}}</h5>
        <a :href="event.url" target="_blank">KUP BILET</a>
      </div>
    </p>
  </div>
</template>

<script>

import axios from 'axios';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: function(){
    return{
      events: []
    }
  },
  methods: {
    getUsers: function() {
      var vm = this;
      axios
        .get("http://app.ticketmaster.com/discovery/v2/events.json?apikey=\tv9Gbr2U1JUFwfeFQBEHmkEAtRZ8PkvxE&city=\"warsaw\"")
        .then(function(response) {
          vm.events = response.data._embedded.events
          console.log(response.data._embedded.events);
        });
    }
  },
  mounted(){
    this.getUsers()
  }
}
</script>

<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}

a {
  color: #42b983;
}
</style>
