<template>
  <transition name="fade">

  <div class="movie-wrapper" :style="styles">
    <div class="movie-info">
      <h1>{{ movie.title }}</h1>
      <span>{{ movie.tagline }}</span>
      <h3>Release Date: {{ movie.release_date }}</h3>
      <p>{{ movie.overview }}</p>
      <hr />
      <h2>Genres</h2>
      <div class="genres">
        <ul>
          <li :key="genre.id" v-for="genre in movie.genres">{{ genre.name }}</li>
        </ul>
      </div>
      <div class="actors">
        <h2>Staring</h2>

        <ul>
          <li :key="credit.id" v-for="credit in movie.credits.cast.splice(0, 2)">{{ credit.name }}</li>
        </ul>
      </div>

    </div>
  </div>
</transition>

</template>

<script>
  const BACKDROP_PATH = "http://image.tmdb.org/t/p/w1280";
  export default {
    data() {
      return {
        movie: {},
      }
    },
    created: function() {
      this.fetchData();
    },
    computed: {
      styles() {
        return {
          background: `url(${BACKDROP_PATH}/${this.movie.backdrop_path}) no-repeat`
        }
      }
    },
    methods: {
      fetchData: async function() {
        try {
          const res = await fetch (`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=1d2eae2beaed7b7d0c046545ec10afb3&append_to_response=credits`);
          const movie = await res.json();
          this.movie = movie;
        } catch (e) {
          console.log(e);
        }
      }
    }
  }

</script>

<style scoped>
.movie-wrapper {
  position: relative;
  padding-top: 50vh;
  background-size: cover;
}
.movie-info {
  background: white;
  color: #222;
  padding: 3rem 10%;
}
.fade-enter-active, .fade-leave-active {
  transition: all .3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
  transform: translateX(100%);
}
.genres {
  ul {
    margin: 0;
    padding: 0;
  }
  li {
    list-style: none;
    display: inline-block;
  }
}
</style>
