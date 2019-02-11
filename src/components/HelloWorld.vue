<template>
  <div class="hello">

      <!--:style="{ backgroundImage: 'url(' + event.images[0].url + ')' }"-->
      <nav>
      <input v-model="city" placeholder="your city">
      <button class="button is-info" @click="getUsers">Check</button>
      </nav>
      <section>
        <div v-for="event in events" class="oneEvent">
          <h1>{{event.name}}</h1>
          <h3>{{event.dates.start.localDate}}</h3>
          <a :href="event.url" target="_blank" class="btn-buy">KUP BILET</a>
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
      city: 'berlin',
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
          console.log(response.data._embedded.events[1].images[1]);
        });
    }
  },
  mounted(){
    this.getUsers()
  }
}
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Libre+Baskerville:400,700&subset=latin-ext');
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800&subset=latin-ext');
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
  padding:100px 0;
  border:1px solid #1976D2;
  background-repeat: no-repeat;
  background-size: cover;
  transition: 1s;
  @media(max-width: 768px){
    width:100%;
  }
  img{
    height:250px;
  }
}
  input{
    border: 0;
    border-bottom: 2px solid #1976D2;
    width: 20%;
    font-size: 30px;
    line-height: 15px;
    height: 40px;
    text-align: center;
    padding: 10px;
    background: transparent;
    color: #BBDEFB;

    &:focus{
      outline: 0;
      color: #BBDEFB
    }
  }
  input::placeholder {
    color: #BBDEFB;
  }
  button{
    background: #1976D2;
    padding: 20px 60px;
    color: #fff;
    text-decoration: none;
    font-size: 1.45em;
    margin: 0 55px;
    outline:none;
    border: 0;
  }
  nav{
    margin:50px 0;
  }
  .btn-buy{
    background-color:#1976D2;
    padding: 20px 40px;
    color:white;
    text-decoration: none;
    border-radius:10px;
    margin-top:50px;
    font-size:12px;
  }
  h3{
    padding-bottom:50px;
    font-family:Montserrat;
    font-weight: 300;
  }
  h1{
    font-size:2em;
    font-family: Libre Baskerville;
    font-weight:700;
  }
</style>
