<template>
  <div class="app">
    <header>
      <h1>Daily<strong>UI</strong></h1>
      <nav></nav>
      <div class="search">
        <svg>
          <use xlink:href="#ico-search"></use>
        </svg>
      </div>
    </header>
    <h2>Most Popular Movies</h2>
    <section class="movies">
      <div class="movie" v-for="movie in movies" :key="movie.title" @click="openDetail(movie)">
        <img :src="movie.poster" alt="" class="poster" />
        <div class="title">{{ movie.title }}</div>
        <div class="info">
          <span class="length">{{ movie.length }}</span>
          <span class="year">{{ movie.year }}</span>
        </div>
        <div class="desc">{{ movie.description }}</div>
      </div>
    </section>
    <div class="detail" v-show="showDetail">
      <svg class="close">
        <use xlink:href="#close"></use>
      </svg>
      <div class="movie">
        <img :src="selectedMovie.poster" alt="" class="poster" />
        <div class="title">{{ selectedMovie.title }}</div>
        <div class="info">
          <span class="length">{{ selectedMovie.length }}</span>
          <span class="year">{{ selectedMovie.year }}</span>
        </div>
        <div class="desc">{{ selectedMovie.description }}</div>
        <button class="play"></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movies: [
        {
          poster: "https://github.com/supahfunk/supah-codepen/blob/master/movie-room.jpg?raw=true",
          title: "Room",
          length: "117 min",
          year: "2015",
          description: "Jack is a young boy of 5 years old who has lived all his life in one room. He believes everything within it are the only real things in the world. But what will happen when his Ma suddenly tells him that there are other things outside of Room?",
        },
        {
          poster: "https://github.com/supahfunk/supah-codepen/blob/master/movie-whiplash.jpg?raw=true",
          title: "Whiplash",
          length: "167 min",
          year: "2015",
          description: "Under the direction of a ruthless instructor, a talented young drummer begins to pursue perfection at any cost, even his humanity.",
        },
        {
          poster: "https://github.com/supahfunk/supah-codepen/blob/master/movie-madmax.jpg?raw=true",
          title: "Mad Max",
          length: "120 min",
          year: "2015",
          description: "An apocalyptic story set in the furthest reaches of our planet, in a stark desert landscape where humanity is broken, and most everyone is crazed fighting for the necessities of life. Within this world exist two rebels on the run who just might be able to restore order. There's Max, a man of action and a man of few words, who seeks peace of mind following the loss of his wife and child in the aftermath of the chaos.",
        },
        {
          poster: "https://github.com/supahfunk/supah-codepen/blob/master/movie-therevenant.jpg?raw=true",
          title: "The Revenant",
          length: "156 min",
          year: "2015",
          description: "In the 1820s, a frontiersman, Hugh Glass, sets out on a path of vengeance against those who left him for dead after a bear mauling.",
        },
      ],
      showDetail: false,
      selectedMovie: {},
    };
  },
  methods: {
    openDetail(movie) {
      console.log(movie);
      this.selectedMovie = movie;
      this.showDetail = true;
    },
    closeDetail() {
      this.selectedMovie = {};
      this.showDetail = false;
    },
  },
};
</script>

<style>
/*--------------------
Body
--------------------*/
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  height: 100vh;
  margin: 0;
  background: radial-gradient(ellipse farthest-corner at center top, #ffee75, #ff8930);
  color: #8b9095;
  font-size: 14px;
  font-family: "Roboto", sans-serif;
}

/*--------------------
App
--------------------*/
.app {
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 640px;
  height: 390px;
  background: #fff;
  border-radius: 15px;
  box-shadow: 0 5px 30px rgba(0, 0, 0, 0.2);
}
.app h2 {
  color: #525661;
  font-size: 17px;
  box-shadow: inset 0 1px 0px rgba(0, 0, 0, 0.1);
  padding: 20px 28px 0;
  margin: -6px 0 0 0;
}

/*--------------------
Header
--------------------*/
header {
  padding: 30px;
  position: relative;
  height: 70px;
}
header h1 {
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 20px;
  text-transform: uppercase;
  text-align: center;
  color: #1c222b;
}
header h1 strong {
  background: #F16018;
  color: #fff;
  display: inline-block;
  border-radius: 30px;
  padding: 6px;
  font-size: 83%;
  line-height: 1;
  position: relative;
  top: -1px;
  left: 2px;
}
header nav {
  cursor: pointer;
  width: 18px;
  height: 18px;
  position: absolute;
  top: 28px;
  left: 28px;
}
header nav::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: #363a47;
  border-radius: 2px;
  box-shadow: 0 5px 0 #363a47, 0 10px 0 #363a47;
}
header .search {
  position: absolute;
  top: 26px;
  right: 18px;
  cursor: pointer;
}
header .search svg {
  width: 20px;
  height: 20px;
}

/*--------------------
Movies
--------------------*/
.movies {
  display: flex;
  padding: 8px 18px;
}
.movies .movie {
  padding: 10px;
  cursor: pointer;
}
.movies .movie .poster {
  width: 100%;
  margin-bottom: 6px;
  border-radius: 4px;
}
.movies .movie .poster.active {
  opacity: 0;
}
.movies .movie .title {
  color: #525661;
  margin-bottom: 4px;
  font-size: 16px;
}
.movies .movie .info {
  font-size: 11px;
  opacity: 0.8;
}
.movies .movie .desc {
  display: none;
}

/*--------------------
Detail
--------------------*/
.detail {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
  padding: 37px 30px 30px 255px;

}
.detail::before {
  content: "";
  background: #fff;
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 15px;
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.67, 0.13, 0.1, 0.81);
}
.detail .close {
  position: absolute;
  top: 21px;
  right: 22px;
  width: 12px;
  height: 12px;
  cursor: pointer;
  border: 6px solid #FFF;
  box-sizing: content-box;
  z-index: 10;
}
.detail .poster {
  position: absolute;
  z-index: 2;
  top: -10%;
  left: -6%;
  height: 100%;
  border-radius: 5px;
  box-shadow: 0 5px 30px rgba(0, 0, 0, 0.2);
  transition: all 0.5s cubic-bezier(0.67, 0.13, 0.1, 0.81);
}
.detail .title,
.detail .info,
.detail .desc,
.detail .play,
.detail .close {
  transform: translateX(-50px);
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.67, 0.13, 0.1, 0.81);
}
.detail .close {
  transform: translateX(10px);
}
.detail .title {
  font-size: 35px;
  font-weight: 300;
  color: #525661;
  margin-bottom: 5px;
}
.detail .info {
  font-size: 11px;
  opacity: 0;
  margin-left: 2px;
}
.detail .desc {
  margin-top: 30px;
  font-size: 14px;
  line-height: 1.6;
}
.detail .play {
  background: linear-gradient(90deg, #E4761F, #FF8B32);
  border: none;
  border-radius: 20px;
  color: #fff;
  font-size: 12px;
  line-height: 1.5;
  padding: 8px 17px;
  margin: 30px 0 0 -2px;
  text-transform: uppercase;
  z-index: 10;
  outline: none !important;
  cursor: pointer;
  opacity: 0;
}
.detail .play svg {
  vertical-align: middle;
  position: relative;
  top: -2px;
  margin-right: 3px;
}

.detail.ready::before {
  opacity: 1;
}
.detail.ready .info {
  opacity: 0.8;
}
.detail.ready .poster {
  opacity: 1;
  transition-duration: 0.5s;
}
.detail.ready .title,
.detail.ready .info,
.detail.ready .desc,
.detail.ready .play,
.detail.ready .close {
  transform: translateX(0);
  opacity: 1;
  transition-delay: 0s;
  transition-duration: 0.5s;
}
.detail.ready .title {
  transition-delay: 0.2s;
}
.detail.ready .info {
  transition-delay: 0.3s;
}
.detail.ready .desc {
  transition-delay: 0.4s;
}
.detail.ready .play {
  transition-delay: 0.5s;
}

.the-most {
  position: fixed;
  z-index: 1;
  bottom: 0;
  left: 0;
  width: 50vw;
  max-width: 200px;
  padding: 10px;
}
.the-most img {
  max-width: 100%;
}
</style>
