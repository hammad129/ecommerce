<template>
  <v-app-bar app color="primary" dark>
    <!-- Navbar toggle button -->
    <v-app-bar-nav-icon @click="toggleSidebar" />

    <!-- Logo -->
    <v-img src="/path/to/logo.png" alt="Logo" class="logo"></v-img>

    <v-spacer></v-spacer>

    <!-- Search Bar -->
    <v-text-field
      v-model="searchQuery"
      label="Search"
      append-icon="mdi-magnify"
      single-line
      hide-details
      class="search-bar"
    ></v-text-field>

    <v-spacer></v-spacer>

    <!-- Login/Signup Buttons -->
    <v-btn  to="/login" text class="login-btn" @click="login">Login</v-btn>
    <v-btn outlined color="white" class="signup-btn" @click="signup">Sign Up</v-btn>

    <!-- Navigation Drawer -->
    <v-navigation-drawer v-model="sidebarOpen" app permanent>
      <v-list>
        <v-list-item v-for="item in sidebarItems" :key="item.title" @click="navigate(item.route)">
          <!-- <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon> -->
          <!-- </v-list-item-icon> -->
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
   
  </v-app-bar>
  <Carosel></Carosel> 
  <Categories></Categories>
  <!-- <Footer></Footer> -->
</template>

<script>

import Carosel from './Carosel.vue';
import Footer from './Footer.vue';
import Categories from './Categories.vue';
export default {
    data() {
        return {
            searchQuery: "",
            sidebarOpen: false,
            sidebarItems: [
                { title: "Home", route: "/home", icon: "mdi-home" },
                { title: "Contact", route: "/contact", icon: "mdi-phone" },
                { title: "About", route: "/about", icon: "mdi-information" },
            ], // Sidebar items
        };
    },
    methods: {
        toggleSidebar() {
            this.sidebarOpen = !this.sidebarOpen;
        },
        navigate(route) {
            // Logic for navigating to the specified route
            this.$router.push(route);
        },
        login() {
            // Logic for login
        },
        signup() {
            // Logic for signup
        },
    },
    components: { Carosel, Categories,Footer }
};
</script>

<style scoped>
.logo {
  height: 40px;
  margin-right: 16px;
}

.search-bar {
  width: 200px;
}

.login-btn {
  margin-right: 8px;
}

.signup-btn {
  margin-left: 8px;
}

@media only screen and (max-width: 600px) {
  /* Mobile responsive styles */
  .logo {
    height: 32px;
    margin-right: 12px;
  }

  .search-bar {
    width: 150px;
  }

  .login-btn,
  .signup-btn {
    font-size: 12px;
    margin: 0;
  }
  .carousel-image {
  height: 400px;
  object-fit: cover;
}

.title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 16px;
}

.description {
  font-size: 16px;
}
}
</style>
