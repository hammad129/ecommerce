<template>
  <v-carousel
    ref="carousel"
    @mouseover="stopCarousel"
    @mouseleave="startCarousel"
  >
    <v-carousel-item v-for="product in carouselItems" :key="product.id">
      <v-img :src="product.thumbnail" :alt="product.title" class="carousel-image"></v-img>
      <v-carousel-item-text>
        <h3 class="title">{{ product.title }}</h3>
        <p class="description">{{ product.description }}</p>
      </v-carousel-item-text>
    </v-carousel-item>
  </v-carousel>

  <div>
    <h2>Product List</h2>

    <v-row class="product-container">
      <v-col v-for="product in paginatedProducts" :key="product.id" cols="6" sm="6" md="4" lg="3">
        <v-card class="product-card" height="100%">
          <v-img :src="product.thumbnail" style="height: 150px" :alt="product.title" class="product-image"></v-img>
          <v-card-title class="product-name">{{ product.title }}</v-card-title>
          <v-card-text class="product-description">{{ product.description }}</v-card-text>
          <v-card-actions>
            <v-btn  to="" color="primary" text>Add to Cart</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>

    <v-pagination
      v-model="currentPage"
      :total-visible="5"
      :length="Math.ceil(products.length / itemsPerPage)"
      prev-icon="mdi-chevron-left"
      next-icon="mdi-chevron-right"
      class="pagination"
    ></v-pagination>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Carousel',
  data() {
    return {
      carouselItems: [],
      intervalId: null,
      currentIndex: 0,
      products: [],
      currentPage: 1,
      itemsPerPage: 10,
    };
  },
  mounted() {
    // Start the carousel timer on mount
    this.startCarousel();

    // Fetch product data from the API
    this.fetchProductData();
  },
  methods: {
    startCarousel() {
      // Clear any existing interval
      this.stopCarousel();

      // Start a new interval to switch images every 5 seconds
      this.intervalId = setInterval(() => {
        this.nextImage();
      }, 5000);
    },
    stopCarousel() {
      // Clear the interval to stop the carousel
      clearInterval(this.intervalId);
    },
    nextImage() {
      // Increment the current index to switch to the next image
      this.currentIndex = (this.currentIndex + 1) % this.carouselItems.length;
    },
    fetchProductData() {
      axios
        .get('https://dummyjson.com/products')
        .then(response => {
          // Extract the product images from the API response
          this.products = response.data.products;
          this.carouselItems = response.data.products.slice(0, 3); // Limit carousel items to the first 3 products
        })
        .catch(error => {
          console.error('Error fetching product data:', error);
        });
    },
  },
  computed: {
    paginatedProducts() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.products.slice(startIndex, endIndex);
    },
  },
};
</script>

<style scoped>
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

.product-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.product-card {
  width: 100%;
  margin-bottom: 20px;
}

.product-image {
  width: 100%;
  height: auto;
}

.product-name {
  font-size: 18px;
  margin-top: 10px;
}

.product-description {
  font-size: 14px;
}

.add-to-cart-btn {
  margin-top: 10px;
}

.pagination {
  margin-top: 16px;
  display: flex;
  justify-content: center;
}
</style>
