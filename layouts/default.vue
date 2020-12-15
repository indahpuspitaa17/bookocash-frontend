<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-container>
        <v-row justify="center" align="center">
          <v-col cols="3">
            <logo />
          </v-col>
          <v-col cols="7" class="black--text">
            <span class="font-weight-bold Poppins">Book O Cash</span>
          </v-col>
        </v-row>
      </v-container>
      <v-divider class="grey lighten-1 mx-4"></v-divider>
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title
              v-text="item.title"
              class="font-weight Poppins"
            />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant"> </v-btn>
      <v-spacer />
    </v-app-bar>

    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>

    <v-footer :absolute="fixed" app>
      <span><b>Indah Puspita</b> &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-view-dashboard",
          title: "Dashboard",
          to: "/dashboard",
        },
        {
          icon: "mdi-desktop-classic",
          title: "Sales",
          to: "/sales",
        },
        {
          icon: "mdi-server",
          title: "Product",
          to: "/product",
        },
        {
          icon: "mdi-archive",
          title: "Inventory",
          to: "/inventory",
        },
        {
          icon: "mdi-poll",
          title: "Reporting",
          to: "/reporting",
        },
        {
          icon: "mdi-store",
          title: "Store Profile",
          to: "/store",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Vuetify.js",
    };
  },
};
</script>
