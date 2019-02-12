<template>
  <div class="hello">
      <!--:style="{ backgroundImage: 'url(' + event.images[0].url + ')' }"-->
      <nav>
        <input v-model="city" placeholder="your city">
        <button class="button is-info" @click="getUsers">Check</button>
      </nav>
      <section>
        <div v-for="(event, index) in events" class="oneEvent" :style="{backgroundColor: color}">
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
      color: 'white',
      isLoading: true,
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
          console.log(response.data._embedded.events);
        });
      setTimeout(() => {
        this.sortedItems();
      },200)
    },
    sortedItems: function() {
      this.events.sort( ( a, b) => {
        return new Date(a.dates.start.localDate) - new Date(b.dates.start.localDate);
      });
      return this.events;
    }
  },
  created(){
    this.getUsers();
  },
  mounted () {
    setTimeout(() => {
      this.isLoading = false
    }, 3000)
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
  width: calc(50% - 4px);
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
    border-bottom: 2px solid white;
    width: 20%;
    font-size: 30px;
    line-height: 15px;
    height: 40px;
    text-align: center;
    padding: 10px;
    background: transparent;
    color: #BBDEFB;

    @media(max-width: 768px){
      width:90%;
      margin-bottom:20px;
    }

    &:focus{
      outline: 0;
      color: #BBDEFB
    }
  }
  input::placeholder {
    color: #BBDEFB;
  }
  button{
    background: white;
    padding: 20px 60px;
    color: #1976D2;
    border-radius:10px;
    text-decoration: none;
    font-size: 1.45em;
    margin: 0 55px;
    outline:none;
    border: 0;
    &:hover{
      cursor:pointer;
    }
  }
  nav{
    margin:50px 0;
  }
  .btn-buy{
    background-color:#1976D2;
    padding: 15px 30px;
    color:white;
    text-decoration: none;
    border-radius:7px;
    margin-top:50px;
    font-size:13px;
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
