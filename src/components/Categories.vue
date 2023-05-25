<template>
    <div>
      <v-container>
        <h2>Product Categories</h2>
        <v-row>
          <v-col v-for="category in categories" :key="category" cols="12" sm="6" md="4" lg="3">
            <v-card class="category-card">
              <v-card-text class="category-name">Category title: {{ category }}</v-card-text>
              <v-btn @click="fetchProductsByCategory(category)" class="view-products-btn" color="primary">View Products</v-btn>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
  
      <v-container>
        <h2>Selected Category: {{ selectedCategory }}</h2>
        <v-row>
          <v-col v-for="product in products" :key="product.id" cols="12" sm="6" md="4" lg="3">
            <v-card class="product-card">
              <v-img :src="product.thumbnail" :alt="product.name" class="product-image"></v-img>
              <v-card-title class="product-name">{{ product.title }}</v-card-title>
              <v-card-text class="product-description">{{ product.description }}</v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'Categories',
    data() {
      return {
        categories: [],
        selectedCategory: '',
        products: [],
      };
    },
    mounted() {
      this.fetchCategories();
    },
    methods: {
      fetchCategories() {
        axios
          .get('https://dummyjson.com/products/categories')
          .then(response => {
            this.categories = response.data;
          })
          .catch(error => {
            console.error('Error fetching categories:', error);
          });
      },
      fetchProductsByCategory(category) {
        this.selectedCategory = category;
  
        fetch(`https://dummyjson.com/products/category/${category}`)
          .then(res => res.json())
          .then(data => {
            this.products = data.products;
          })
          .catch(error => {
            console.error('Error fetching products:', error);
          });
      },
    },
  };
  </script>
  
  <style scoped>
  .category-card {
    border: 1px solid #ccc;
    padding: 16px;
    margin-bottom: 16px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  
  .category-name {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 8px;
  }
  
  .view-products-btn {
    margin-top: auto;
  }
  
  .product-card {
    margin-bottom: 16px;
  }
  
  .product-image {
    height: 200px;
    object-fit: cover;
  }
  
  .product-name {
    font-size: 16px;
    font-weight: bold;
    margin-bottom: 8px;
  }
  
  .product-description {
    color: #666;
  }
  </style>
  