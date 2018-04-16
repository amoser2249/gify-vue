<template>
  <div id="app">
  <section class="hero is-fullheight">
  <div class="hero-body">
    <div class="container">
      <h1 class="title">Amazing Gif Searcher</h1>
      <div class="field is-grouped">
        <div class="control has-icons-left">
          <input v-model="searchTerm" type="text" class="input is-warning" placeholder="Search" @keyup.enter="getGifs()">
          <span class="icon is-left">🔮</span>
        </div>
        <div class="control">
          <button class="button" @click="getGifs()">Go</button>
        </div>
      </div>
      <section class="gif-container">
        <div v-for="gif in gifs" :key="gif.id">
          <img :src="gif">
        </div>
      </section>
    </div>
  </div>
</section>
</div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: "",
      gifs: []
    };
  },
  methods: {
    getGifs() {
      let apiKey = "dc6zaTOxFJmzC";
      let searchEndPoint = "https://api.giphy.com/v1/gifs/search?";
      let limit = 5;

      let url = `${searchEndPoint}&api_key=${apiKey}&q=${
        this.searchTerm
      }&limit=${limit}`;
      
      fetch(url)
        .then(response => {
          return response.json();
        })
        .then(json=> {
          this.buildGifs(json);
        })
        .catch(err => {
          console.log(err);
        })
    },
    buildGifs(json) {
      this.gifs = json.data
        .map(gif => gif.id)
        .map(gifId => {
          return `https://media.giphy.com/media/${gifId}/giphy.gif`;
      });
    }
  }
};
</script>

<style>
.hero {
  background: linear-gradient(-30deg, #cf215be5, #cf215be5 45%, #cf215b 45%)
    #fff;
}
.hero-body h1 {
  color: #ffffff;
}

.box {
  text-align: center;
}
</style>
