<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../../components/Joke";
import SearchJokes from "../../components/SearchJokes";

export default {
  components: {
    Joke,
    SearchJokes
  },
  data() {
    return {
      jokes: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };

    try {
      const response = await axios.get(
        "https://icanhazdadjoke.com/search",
        config
      );

      this.jokes = response.data.results;

      console.log(response.data);
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      };

      try {
        const response = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        );

        this.jokes = response.data.results;

        console.log(response.data);
      } catch (error) {
        console.log(error);
      }
    }
  },
  head() {
    return {
      title: "Dad Jokes"
    };
  }
};
</script>

<style>
</style>