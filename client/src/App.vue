<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" fixed app>
      <v-list-item>
        <v-list-item-avatar>
              <v-img src="@/assets/avatar.png"></v-img>
            </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title> SK12 </v-list-item-title>
          <v-list-item-subtitle> SUPERHEROES APP </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-divider />
      <v-list dense>
        <v-list-item-group color="teal darken-2">
          <v-list-item v-for="(item, i) in items" :key="i" :to="item.link" link>
            <v-list-item-icon>
              <v-icon v-text="item.icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app color="teal darken-4" dark>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title style="font-weight:bold;font-size:1.8em;">SUPERHEROES</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
    <v-footer color="teal darken-4" dark>
      <v-col class="text-center" cols="12" style="font-size:1.1em;">
       © {{ new Date().getFullYear() }} — <strong>SUPERHEROES - All Rights Reserved</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    items: [
      { title: "Home", icon: "mdi-home", link: "/" },
      { title: "Create New Post", icon: "mdi-note-plus", link: "/add-post" },
      { title: "About", icon: "mdi-help-box", link: "/about" },
    ],
  }),
};
</script>