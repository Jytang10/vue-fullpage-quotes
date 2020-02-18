<template>
  <div id="app">
    <full-page v-if="isLoaded" :options="options" id="fullpage">
      <div v-for="quote in quotes" :key="quote.data.id" class="section">
        <div class="container">
          <img
            src="./assets/positivity.svg"
            alt="positivity icon"
            class="quote-img"
          />
          <div class="quote-symbol">“</div>
          <p class="quote">
            <a :href="quote.data.url">{{ quote.data.title }}</a>
          </p>
          <div class="details">
            <div class="details-author">Contributor: {{quote.data.author}}</div>
            <div class="details-stats">{{quote.data.ups}} Up Votes | {{quote.data.num_comments}} Comments</div>
          </div>
        </div>
      </div>
    </full-page>
    <div v-else><LoadingSpinner /></div>
  </div>
</template>

<script>
import LoadingSpinner from "@/components/LoadingSpinner.vue";
export default {
  name: "App",
  components: { LoadingSpinner },
  created() {
    fetch("https://www.reddit.com/r/quotes.json?limit=20")
      .then(res => res.json())
      .then(data => {
        this.quotes = data.data.children;
        // this.quotes.shift();
        // this.quotes.shift();
        this.isLoaded = true;
      });
  },
  data() {
    return {
      isLoaded: false,
      quotes: [],
      options: {
        scrollBar: true,
        sectionsColor: [
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401",
          "#1bcee6",
          "#ee1a59",
          "#ba5be9",
          "#b4b8ab",
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401",
          "#1bcee6",
          "#ee1a59",
          "#ba5be9",
          "#b4b8ab",
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401"
        ]
      }
    };
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Sriracha&display=swap");
#app {
  font-family: sans-serif;
  color: #2d3748;
}

body {
  margin: 0;
  padding: 0;
}

h3 {
  margin: 0;
}

.container {
  margin: auto;
  max-width: 800px;
  padding: 80px 16px;
}

.section {
  text-align: center;
}

.quote-img {
  width: 25%;
}

.quote-symbol {
  font-size: 64px;
  line-height: 0;
  margin-top: 50px;
  color: white;
}

.quote a {
  text-decoration: none;
  font-family: "Sriracha", cursive;
  color: white;
  font-size: 36px;
  line-height: 1.5;
}

.quote a:hover {
  color: #edf2f7;
}

.details {
  font-size: 25px;
}

.details-stats {
  margin-top: 4px;
}
</style>
