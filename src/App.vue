<template>
  <div id="app">
    <Cockpit
      @onSearchList="searchList"
      @onSortList="sortList"
    />
    <List
      :movies="displayedList"
      @onSelectMovie="selectMovie"
    />
    <Single
      :selected="selectedMovie"/>
  </div>
</template>

<script>
import Cockpit from './components/Cockpit.vue';
import List from './components/List.vue';
import Single from './components/Single.vue';
import axios from "axios";

export default {
  name: 'App',
  components: {
    Cockpit,
    List,
    Single
  },
  data() {
    return {
      movieList: [],
      displayedList: [],
      selectedMovie: {}
    }
  },
  mounted() {
    axios.get('https://star-wars-api.herokuapp.com/films')
    .then( res => {
      this.movieList = res.data;
      this.displayedList = res.data;
    })
    .catch(err => console.log('Failed to fetch data', err))
  },
  methods: {
    selectMovie(id){
      const selected = this.movieList.filter( mov => {
        return mov.id === id;
      });
      return this.selectedMovie = { ...selected[0] };
    },
    searchList(e){
      const query = e.currentTarget.value.toLowerCase();
      this.query = query;
      let resultList = this.movieList.filter(mov => mov.fields.title.toLowerCase().includes( query ));
      return this.displayedList = resultList;
    },
    sortList(property){
      const sortedList = this.movieList.sort((a, b) => {
        if (a.fields[property] < b.fields[property]) {
          return -1;
        }
        if (a.fields[property] > b.fields[property]) {
          return 1;
        }
        return 0;
      });

      this.movieList = sortedList;

      if( this.query ){
        return this.displayedList = sortedList.filter(mov => mov.fields.title.toLowerCase().includes( this.query ));
      }

      return this.displayedList = sortedList;
    }
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;800&display=swap');

body{
  margin: 0;
}

#app {
  display: flex;
  flex-wrap: wrap;
  font-family: 'Open Sans', sans-serif;
}
</style>
