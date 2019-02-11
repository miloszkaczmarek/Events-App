<template>
  <div class="hello">
    <p>
      <input v-model="city" placeholder="your city">
      <button class="button is-info" @click="getUsers">Get Repos</button>
      <h5>{{ city }}</h5>
      <section>
        <div v-for="event in events" class="oneEvent" :style="{ backgroundImage: 'url(' + event.images[0].url + ')' }">
          <img :src="event.images[0].url" alt="">
          <h5>{{event.name}}</h5>
          <h5>{{event.dates.start.localDate}}</h5>
          <a :href="event.url" target="_blank">KUP BILET</a>
        </div>
      </section>
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
      events: [],
      city: 'berlin'
    }
  },
  methods: {
    getUsers: function() {
      var vm = this;
      let repoUrl = 'http://app.ticketmaster.com/discovery/v2/events.json?apikey=\tv9Gbr2U1JUFwfeFQBEHmkEAtRZ8PkvxE&city=' + this.city;
      axios
        .get(repoUrl)
        .then(function(response) {
          vm.events = response.data._embedded.events
          console.log(response.data._embedded.events[1].images[0].url);
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
section{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.oneEvent{
  background-color: white;
  width: calc(50% - 2px);
  padding:50px 0;
  border:1px solid black;
  background-repeat: no-repeat;
  background-size: cover;
  @media(max-width: 768px){
    width:100%;
  }
  img{
    height:250px;
  }
}
</style>
