<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
    <!--Avatar-->
    <v-layout column align-right>
      <v-list>
        <v-list-item>
              <v-list-item-avatar>
                <img
                  src="../assets/logo.png"
                  alt="Indah"
                >
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>Book O Cash</v-list-item-title>
              </v-list-item-content>
          </v-list-item>
        </v-list>
    </v-layout>

    <v-divider class="mx-4"></v-divider>
    
      <v-list
        dense
        rounded>
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
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <template v-slot:append>
        <div class="pa-2">
          <v-btn block>
            Logout
          </v-btn>
        </div>
      </template>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />    
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }} — <strong>Indah Puspita</strong></span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-view-dashboard',
          title: 'Dashboard',
          to: '/'
        },
        {
          icon: 'mdi-sale',
          title: 'Sales',
          to: '/sales'
        },
        {
          icon: 'mdi-briefcase',
          title: 'Product',
          to: '/product'
        },
        {
          icon: 'mdi-cart',
          title: 'Inventory',
          to: '/inventory'
        },
        {
          icon: 'mdi-book-open',
          title: 'Reporting',
          to: '/reporting'
        },
        {
          icon: 'mdi-account',
          title: 'Store Profile',
          to: '/storeProfile'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>
