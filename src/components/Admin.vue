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
          outlined
          dense
          solo-inverted
          prepend-inner-icon="mdi-magnify"
          @keyup.enter="search"
      ></v-text-field>
  
      <v-spacer></v-spacer>
  
      <!-- Login/Signup Buttons -->
      <v-btn  to="/" text class="login-btn" @click="login">Log out</v-btn>
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
    <div>
    <h2>Product List</h2>
    <v-row class="product-container">
      <v-col v-for="product in searchResults" :key="product.id" cols="6" md="6" lg="3">
        <v-card class="" height="100%">
          <v-img :src="product.thumbnail" :alt="product.name" class="product-image " style="height:200px;" cover></v-img>
          <v-card-title class="product-name">{{ product.title }}</v-card-title>
          <v-card-text class="product-description">{{ product.description }}</v-card-text>
          <v-card-actions>
            <v-btn color="primary" text>Add to Cart</v-btn>
            <v-btn color="primary" text @click="editProduct(product)">Edit</v-btn>
            <v-btn color="primary" text @click="deleteProduct(product)">Delete</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
    </template>
    <script>
    import axios  from 'axios';
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
            searchResults : [],
        };
    },
    onBeforeMount()
    {
        this.search();
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
       async search() {
      await axios
        .get(`https://dummyjson.com/products/search?q=${this.searchQuery}`)
        .then(response => {
          this.searchResults = response.data.products;
          console.log(this.searchResults);
        })
        .catch(error => {
          console.error('Error searching:', error);
        });
    }
    },
}

</script>