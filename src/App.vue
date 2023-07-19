<template>
  <v-app id="app">
    <v-navigation-drawer v-model="drawer" :permanent="$vuetify.breakpoint.lgAndUp" app>
      <v-list-item class="mx-auto">
        <v-list-item-avatar>
          <v-img src="https://randomuser.me/api/portraits/men/85.jpg"></v-img>
        </v-list-item-avatar>
        <v-list-item-title>
          <div class="h4 mx-2 text-start">User</div>
        </v-list-item-title>
      </v-list-item>

      <v-divider class="m-0"></v-divider>
      <v-list>
        <v-list-item v-for="(item, index) in navItems" :key="index" link class="sidebarMenu"
          :class="{ 'active-tab': index === activeTabIndex }" active-class="active-tab">
          <v-list-item-icon>
            <v-icon :style="{ color: index === activeTabIndex ? '#E81A89' : '' }">{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content class="text-start font-weight-medium">
            <v-list-item-title class="logo-text">{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon  v-if="$vuetify.breakpoint.mdAndDown" @click.prevent="drawer = !drawer"></v-app-bar-nav-icon>
      <div :class="$vuetify.breakpoint.mdAndDown ? 'h5' : 'h4' " class="d-inline mb-0 text-muted">
        Dashboard
      </div>

      <v-spacer></v-spacer>
      <div class="d-flex align-items-center justify-content-between">
        <div class="px-0">
          <v-btn icon>
            <v-icon>mdi-account</v-icon>
          </v-btn>
        </div>
        <div class="px-0">
          <v-btn icon>
            <v-badge :content="messages" :value="messages" color="green" overlap>
              <v-icon class="text-primary">mdi-bell</v-icon>
            </v-badge>
          </v-btn>
        </div>
        <div class="px-0">
          <v-btn icon>
            <v-icon>mdi-cog</v-icon>
          </v-btn>
        </div>
      </div>
    </v-app-bar>

    <v-main>
      <DashboardPage></DashboardPage>
    </v-main>
  </v-app>
</template>

<script>
import DashboardPage from './pages/DashboardPage.vue'
export default {
  name: 'App',
  components: {
    DashboardPage
  },
  data() {
    return {
      drawer: false,
      navItems: [
        { title: 'Dashboard', icon: 'mdi-view-dashboard' },
        { title: 'Profile', icon: 'mdi-account' },
        { title: 'Cards', icon: 'mdi-card' },
        { title: 'Analytics', icon: 'mdi-chart-bar' },
        { title: 'Community', icon: 'mdi-account-group' },
        { title: 'Notifications', icon: 'mdi-bell' },
      ],
      activeTabIndex: 0,
      messages: 10,
    };
  }
}
</script>

<style>
#app {
  font-family: Poppins, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #f9f9f9;
}

v-col {
  padding: 0 !important;
}

.active-tab {
  border-left: 4px solid #E81A89;
  background-color: #f9f9f9;
}

.sidebarMenu:hover {
  background-color: #f9f9f9;
}
</style>
