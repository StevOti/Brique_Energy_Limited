<template>
  <div class="home">
    <section class="hero mb-6 columns is-flex is-flex-direction-row is-align-items-center">
      <!-- Left half -->
      <div class="column is-half is-flex is-justify-content-center is-hidden-mobile">
        <div>
          <p class="title mb-4 is-size-2">
            Our newest innovation is here.
          </p>
          
          <p class="mb-6">
            Introducing the new briquettes, where quality meets innovation in briquette and shisha charcoal production. We're dedicated to excellence and sustainability, ensuring top-tier products and unmatched service. 
            Elevate your grilling and shisha experience with us.
          </p>

          <router-link to="/search" class="buttons">
            <a href="#" class="button is-black">Shop Now</a>
          </router-link>
        </div>
      </div>

  <!-- Right half -->
  <div class="column is-half is-flex is-justify-content-center">
    <img src="../assets/Coconut-Charcoal-_Briquette.png" alt="Image">
  </div>
</section>

<!-- Mobile version -->
<div class="column is-12 is-flex is-justify-content-center is-align-items-center is-mobile is-hidden-desktop">
  <div>
    <p class="title mb-6 is-size-4 is-bolder">
      Our newest innovation is here.
    </p>
    <p>
      Introducing the new briquettes, where quality meets innovation in briquette and shisha charcoal production. We're dedicated to excellence and sustainability, ensuring top-tier products and unmatched service. 
      Elevate your grilling and shisha experience with us.
    </p>
  </div>
</div>


<div class="container is-flex is-flex-wrap-wrap is-justify-content-center my-16 pb-6">
  <div class="is-flex is-align-items-center mb-4">
    <img src="../assets/logoipsum-211.svg" alt="Brand 1" width="132" height="35" class="mr-6">
    <img src="../assets/logoipsum-221.svg" alt="Brand 2" width="119" height="30" class="mr-6">
    <img src="../assets/logoipsum-225.svg" alt="Brand 3" width="49" height="48" class="mr-6">
    <img src="../assets/logoipsum-280.svg" alt="Brand 4" width="78" height="30" class="mr-6">
    <img src="../assets/logoipsum-284.svg" alt="Brand 5" width="70" height="44" class="mr-6">
    <img src="../assets/logoipsum-215.svg" alt="Brand 6" width="132" height="40">
  </div>
</div>



    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="title is-size-2 is-bolder">Latest Products</h2>

        <p>
          Discover our latest products, where innovation meets quality. From premium grilling briquettes to 
          top-of-the-line shisha charcoal, each offering is meticulously crafted to elevate your experiences. 
          Whether you're a barbecue enthusiast, shisha connoisseur, or industrial professional, 
          our newest additions promise unrivaled performance and satisfaction. Stay ahead of the curve and 
          explore our latest innovations to ignite your passions and enhance every moment.
        </p>

      </div>
      
      <ProductBox
      v-for="product in latestProducts"
      v-bind:key="product.id"
      v-bind:product="product"/>

    </div>

    <div class="pt-6 pb-6">
      <div class="columns is-multiline is-mobile">
      <div class="column is-3-desktop is-6-tablet is-12-mobile" v-for="(card, index) in cards" :key="index">
        <div class="card" style="border-radius: 16px;">
          <div class="card-content p-6">
            <div class="media">
              <div class="media-left">
                <figure class="image is-48x48 is-flex is-justify-content-center is-align-items-center">
                  <router-link to="/cart" class="nav-button">
                    <span class="icon is-size-3">
                      <i :class="card.icon" style="color: orange;"></i>
                    </span>
                  </router-link>
                </figure>
              </div>
              <div class="media-content pl-4">
                <p class="title is-4">{{ card.title }}</p>
                <p class="subtitle is-6">{{ card.subtitle }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import ProductBox from '@/components/ProductBox';


export default {
  name: 'HomeView',
  data() {
    return {
      latestProducts: [],
      cards: [
          {
            title: 'Free Shipping',
            subtitle: 'Free shipping on order under €50',
            icon: 'fas fa-truck'
          },
          {
            title: 'Peace of Mind',
            subtitle: '30 days money back guarantee',
            icon: 'fas fa-undo'
          },
          {
            title: 'Secured Payment',
            subtitle: 'Your payment are safe with us.',
            icon: 'fas fa-lock'
          },
          {
            title: 'Support 24/7',
            subtitle: '24/7 Online customer support',
            icon: 'fas fa-headset'
          }
        ]

    }
  },
  components: {
    ProductBox
  },
  mounted() {
    this.getLatestProducts()

    document.title =  'Home | CKLove&Light'
  },
  methods: {
    getLatestProducts() {
      axios
      .get('/api/v1/latest-products')
      .then(response =>{
        this.latestProducts = response.data
      })
      .catch(error => {
        console.log(error)
      })
    }
  }
}
</script>