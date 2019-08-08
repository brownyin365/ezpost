<template>
  <v-layout row wrap align-center>
    <v-card-title class="title">
      <v-card-text class="headline"
        ><h1>Fat News Around the Globe</h1></v-card-text
      >
    </v-card-title>
    <v-flex xs8 offset-md2>
      <div v-for="article in articles" :key="article.title">
        <v-card class="my-3" hover>
          <v-img height="350px" v-bind:src="article.urlToImage"></v-img>
          <v-container fill-height fluid>
            <v-layout>
              <v-flex xs12 align-end d-flex>
                <span class="headline">{{ article.title }}</span>
              </v-flex>
            </v-layout>
          </v-container>
          <v-card-text>
            {{ article.description }}
          </v-card-text>
          <v-card-actions>
            <v-chip small color="secondary" class="white--text">
              {{ article.source.name }}
            </v-chip>
            <v-spacer></v-spacer>
            <v-btn icon class="red--text">
              <v-icon small>fab fa-reddit</v-icon>
            </v-btn>
            <v-btn icon class="light-blue--text">
              <v-icon small>fab fa-twitter</v-icon>
            </v-btn>
            <v-btn icon class="blue--text text--darken-4">
              <v-icon small>fab fa-facebook-f</v-icon>
            </v-btn>
            <v-btn icon class="red--text">
              <v-icon small>fab fa-google-plus</v-icon>
            </v-btn>
            <v-btn icon class="blue--text text--darken-4">
              <v-icon small>fab fa-linkedin</v-icon>
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn
              small
              replace
              color="#f50057"
              v-bind:href="article.url"
              target="_blank"
              >Read More</v-btn
            >
          </v-card-actions>
        </v-card>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      drawer: false,
      api_key: "478a527bd6774473a4e5c21285d26a13",
      articles: [],
      errors: []
    };
  },
  created() {
    axios
      .get(
        "https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=" +
          this.api_key
      )
      .then(response => {
        //this.articles = response.data.articles
        this.articles = response.data.articles;
        console.log("data:");
        console.log(response.data.articles); // This will give you access to the full object
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>
<style></style>
