<template>
    <v-card class="login-card">
      <v-card-title class="login-title">Login</v-card-title>
      <v-card-text>
        <v-form @submit="login">
          <v-text-field
            v-model="username"
            label="Username"
            outlined
            required
          ></v-text-field>
          <v-text-field
            v-model="password"
            label="Password"
            type="password"
            outlined
            required
          ></v-text-field>
          <v-btn type="submit" color="primary">Login</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        username: '',
        password: ''
      };
    },
    methods: {
      login() {
        // Make the API call to authenticate the user
        axios
          .post('https://dummyjson.com/auth/login', {
            username: this.username,
            password: this.password
          })
          .then(response => {
            // Handle the authentication response
            console.log(response.data);
            // Redirect to the admin dashboard
            this.$router.push('/admin');
          })
          .catch(error => {
            // Handle the authentication error
            console.error(error);
            // Display an error message or take appropriate action
          });
      }
    }
  };
  </script>
  
  <style scoped>
  .login-card {
    max-width: 400px;
    margin: auto;
    padding: 20px;
  }
  
  .login-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  </style>
  