<template>
  <div id="app" class="container">
    <div v-if="loaded">
      <div class="header"><h2>🎥</h2></div>

      <div class="item movieInfo">
        <div class="poster"><img v-if="foto" :src="foto" /></div>
        <div class="text">
          <h5 class="movie-title">{{ title }}</h5>
          <h5 class="year">{{ year }}</h5>
          <h6 class="genre">{{ genre }}</h6>
          <p class="plot">{{ plot }}</p>
        </div>
      </div>

      <div class="item input">
        <form @submit.prevent="searchMovie()">
          <label for="movieName" class="mr-2">Movie name</label><br />
          <input
            v-model="movieQuery"
            type="search"
            inputmode="search"
            class="form-control col-md-30"
            id="movieInput"
            placeholder="Three Billboards Outside Ebbing, Missouri"
            aria-describedby="movieSearchHelp"
          />
          <small id="movieSearchHelp" class="form-text text-muted">Search for a movie</small>
          <!-- <button type="submit">Submit</button> -->
        </form>
      </div>


      <!-- <p v-if="movie" class="d-flex justify-content-md-center mt-3">You are adding&nbsp; <a v-bind:href="imdbLink"><b>{{ title }}</b></a>&nbsp; by director&nbsp;  <b>{{ director }}</b>, released in&nbsp;<b>{{ year }}</b>.</p> -->

      <ul style="list-style: none">
        <li v-for="(item, index) in moviesList" :key="item">
          <span>{{ index + 1 }}</span
          ><a v-on:click="selectMovie(index)">{{ item.Title }}</a>
          <!-- <form class="form-inline" @submit.prevent="selectMovie(index)">
          <button type="submit" class="">👉</button>
          <label for="movieName" class="mr-2">{{ item.Title }}</label>
        </form> -->
        </li>
      </ul>

      <!-- <div class="item search-box">
      <form @submit.prevent="searchMovie()">
        <div class="form-group">
          <label for="movieName">Movie name</label>
          <input
            v-model="movieQuery"
            type="text"
            class="form-control"
            id="movieInput"
            aria-describedby="movieSearchHelp"
            placeholder="Search for a movie"
          />
          <small id="movieSearchHelp" class="form-text text-muted">Search for a movie</small>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  mounted() {
    console.log("mounted");
    this.searchMovie(this.movieQuery);
    this.$nextTick(() => {
      // Fires before full page is rendered
      this.loaded = true;
    });
  },
  data() {
    return {
      loaded: false,
      selectedIndex: -1,
      movieQuery: "Three Billboards Outside Ebbing, Missouri",
      movie: {},
      foto: "",
      title: "",
      plot: "",
      genre: "",
      imdbLink: "",
      director: "",
      year: "",
      moviesList: [],
    };
  },
  methods: {
    searchMovie() {
      fetch("https://www.omdbapi.com/?apikey=2d1ccbe&s=" + this.movieQuery)
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          this.moviesList = data.Search;
          data = this.moviesList[0];
          fetch("https://www.omdbapi.com/?apikey=2d1ccbe&i=" + data.imdbID)
            .then((response) => {
              return response.json();
            })
            .then((data) => {
              console.log(data);
              this.foto = data.Poster;
              this.title = data.Title;
              this.plot = data.Plot;
              this.genre = data.Genre;
              this.imdbLink = "https://www.imdb.com/title/" + data.imdbID;
              this.director = data.Director;
              this.year = data.Year;
            });
        });
      this.movieQuery = "";
    },
    selectMovie(index) {
      this.selectedIndex = index;
      this.movie = this.moviesList[index];
      fetch("https://www.omdbapi.com/?apikey=2d1ccbe&i=" + this.movie.imdbID)
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          console.log(data);
          this.foto = data.Poster;
          this.title = data.Title;
          this.plot = data.Plot;
          this.genre = data.Genre;
          this.imdbLink = "https://www.imdb.com/title/" + data.imdbID;
          this.director = data.Director;
          this.year = data.Year;
        });
    },
  },
  created: function () {
    this.searchMovie();
  },
};
</script>

<style scoped>
.container {
  display: grid;
  grid-template-columns: 100%;
  grid-template-rows: 80px auto 50px;
}

.item {
  /* border:1px solid black; */
}
/* img {
  display: block;
  margin: auto;
  width: 20rem;
} */

.movieInfo {
  grid-row: 2;
  grid-column: 1;
  display: grid;
  grid-template-columns: 3fr auto;
  grid-template-rows: 25% 25% 25% 25%;
  /* border:1px solid white; */
  /* margin: auto;
  max-width:90%;
  min-height: 300px; */
  /* border: 1px solid black; */
  /* background: lightcoral; */
  /* border: 5px solid red; */
}

form {
  margin-top: 1rem;
}

input {
  width: 70%;
  height: 2rem;
  margin-top: 0.5rem;
  margin-bottom: 1rem;
}

ul {
  padding-top: 1rem;
  font-size: 1.5rem;
  text-align: left;
}

ul > li:nth-child(even) {
  color: grey;
}

ul button {
  margin: 0 10px;
}

ul a {
  margin: 0 10px;
}

ul a:hover {
  /* display:none; */
}
.poster {
  grid-template-columns: 1;
  grid-row: 1/4;
  /* float:left;
border: 5px solid red; */
  /* width:50px; */
}

.poster img {
  max-width: 200px;
}

.movieInfo .text {
  /* grid-column:2; */
}
.movieInfo .movie-title {
  grid-row: 1;
  grid-column: 2;
  align-self: top;
  margin-top: 5px;
  margin-bottom: 5px;
  /* border: 1px solid white; */
}

.movieInfo .genre {
  margin-top: 0;
  margin-bottom: 10px;
  font-style: italic;
  color: darkgray;
}

.movieInfo .plot {
  font-size: 0.9rem;
  margin: 0 15px;
  text-align: left;
  /* text-justify: inter-word; */
}

.movieInfo .year {
  margin: 0 0 10px 0;
}

.search-box {
  grid-row: 4;
}

.header {
  grid-row: 1;
  align-self: top;
}
</style>
