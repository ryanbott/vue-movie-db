<template >
  <ul>
    <li :key="movie.id" v-for="movie in movies.slice(0, 18)">
      <Movie :movie="movie"/>
    </li>
  </ul>
</template>

<script>
  import Movie from './Movie.vue';

  export default {
    name: 'MoviesList',
    data() {
      return {
        movies: []
      }
    },
    beforeCreate() {
      console.log('before create')
    },

    created: function() {
      console.log('created!!')

      this.fetchData();
    },

    beforeMount() {
      console.log('before mount')
    },
    mounted() {
      console.log('mounted')
    },
    beforeUpdate() {
      console.log('beforeUpdate')
    },
    updated() {
      console.log('updated')
    },
    methods: {
      fetchData: async function() {
        try {
          const res = await fetch ('https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=1d2eae2beaed7b7d0c046545ec10afb3');
          const movies = await res.json();
          this.movies = movies.results;
        } catch (e) {
          console.log(e);
        }
      }
    },
    components: {
      Movie
    },
  };

</script>

<style scoped>
ul {
  display: grid;
  list-style: none;
  padding: 1rem;
  margin: 0;
  grid-row-gap: 1rem;
  grid-template-columns: repeat(6, 1fr);
}

</style>
