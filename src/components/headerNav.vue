<template>
  <div class="d-flex w-100">
    <v-container fluid class="white sticky-header">
      <v-row>
        <nuxt-link to="/" class="ma-0 pa-0 d-flex black--text">
          <v-col class="align-self-center">
            <h1 class="d-flex">My Portfolio</h1>
          </v-col>
        </nuxt-link>
        <v-spacer />
        <v-col align="right">
          <v-btn color="light" fab elevation="0" @click="drawer = !drawer">
            <v-icon>mdi-menu</v-icon>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>

    <!-- navigation -->
    <v-navigation-drawer v-model="drawer" bottom right absolute temporary>
      <v-list nav dense>
        <h2 class="py-3">Navigation</h2>

        <!-- solo pages -->
        <v-list-item-group active-class="deep-purple--text text--accent-4">
          <v-list-item :to="'/'">
            <v-list-item-title> Home Page </v-list-item-title>
          </v-list-item>
        </v-list-item-group>

        <v-divider></v-divider>
        <!-- projects -->
        <v-list-item-group active-class="deep-purple--text text--accent-4">
          <v-list-item
            v-for="project in projects"
            :key="project.slug"
            :to="'/projects/' + project.slug"
          >
            <v-list-item-title>
              {{ project.title }}
            </v-list-item-title>
          </v-list-item>
        </v-list-item-group>
        <v-divider></v-divider>
      </v-list>
    </v-navigation-drawer>

    <div class="sticky-padding">&nbsp;</div>
  </div>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    projects: [],
  }),
  async fetch() {
    this.projects = await this.$content('projects')
      .sortBy('path')
      .fetch()
      .catch((error) => console.error(error))
  },
}
</script>

<style lang="scss">
@import 'assets/styles/variables.scss';
.sticky-header {
  top: 0;
  position: fixed;
  z-index: 1;
  a {
    color: black;
    text-decoration: none;
  }
}
.sticky-padding {
  height: $header-height;
}
</style>