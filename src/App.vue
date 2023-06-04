<template>
  <v-app style="background-color: black">
    <Nav></Nav>

    <div class="banner">
      <v-img :src="getImageUrl('banner.PNG')" alt="banner"></v-img>
    </div>

    <v-main>
      <v-container fluid>
        <Home> </Home>
      </v-container>
    </v-main>

    <Footer> </Footer>
  </v-app>
</template>

<style>
.banner {
  margin-top: 64px;
}
</style>

<script>
import Nav from "./components/Nav.vue";
import Home from "./components/Home.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Nav,
    Home,
    Footer,
  },
  methods: {
    getImageUrl(imagePath) {
      return window.location.origin + "/" + imagePath;
    },
  },
};
</script>
