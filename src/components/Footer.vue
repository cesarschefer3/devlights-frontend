<template>
  <v-footer color="rgb(53 53 53)">
    <v-container>
      <v-row align="center">
        <v-col cols="auto">
          <v-toolbar-title class="icon">MS Icon</v-toolbar-title>
        </v-col>
        <v-col class="text-center">
          <span class="white--text">
            <v-btn
              v-for="link in links"
              :key="link"
              color="white"
              variant="text"
              rounded="xl"
              small
              class="footer-buttons"
            >
              {{ link }} |
            </v-btn>
          </span>
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>

<style>
  .icon{
    color:white;
  }
  .footer-buttons{
     font-size: 10px;
  }
</style>

<script>
export default {
  data: () => ({
    links: ["Acerca de Valve", "Steamworks", "Distribución de Steam", "Tarjetas regalo", "Steam", "@steam"],
  }),
};
</script>