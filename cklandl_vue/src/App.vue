<template>
  <div id="wrapper">

    <nav class="navbar is-light">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item">
          <i class="fas fa-fire p-4" style="font-size: 24px; color: orange;"></i>
          <p class="navbar-logo">
            Brique Energy<span class="nav-logo-item">.</span>
          </p>
        </router-link>
        <!-- Updated toggle button with correct data-target -->
        <a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <!-- Updated mobile menu with conditional class -->
      <div class="navbar-menu" id="navbar-menu" :class="{ 'is-active': showMobileMenu }" style="justify-content: center; align-items: center;">
        <div class="navbar-start pl-6">
          <router-link to="/" class="navbar-item">Home</router-link>
          <router-link to="/About" class="navbar-item">About</router-link>
          <router-link to="/Search" class="navbar-item">Products</router-link>
          <router-link to="/Contact" class="navbar-item">Contact Us</router-link>
        </div>
        
        <div class="navbar-end is-flex">

          <div class="navbar-start">
            <div class="navbar-item">
              <form method="get" action="/search">
                <div class="field has-addons">
                  <div class="control has-icons-left">
                    <input type="text" class="input is-expanded" placeholder="Search here" name="query">
                    <span class="icon is-left">
                      <i class="fas fa-search"></i>
                    </span>
                  </div>
                </div>
              </form>
            </div>
          </div>

          <div class="navbar-item">
            <router-link to="/cart" class="nav-button">
              <span class="icon"><i class="far fa-heart" style="color: black;"></i></span>
            </router-link>
          </div>
          
          <div class="navbar-item">
            <template v-if="$store.state.isAuthenticated">
              <router-link to="/my-account" class="nav-button">
                <span class="icon"><i class="far fa-user" style="color: black;"></i></span>
              </router-link>
            </template>
            <template v-else>
              <router-link to="/log-in" class="nav-button">
                <span class="icon"><i class="far fa-user" style="color: black;"></i></span>
              </router-link>
            </template>
          </div>

          <div class="navbar-item">
            <router-link to="/cart" class="nav-button">
              <span class="icon"><i class="far fa-shopping-cart" style="color: black;"></i></span>
              <span style="color: black;">({{ cartTotalLength }})</span>
            </router-link>
          </div>
        </div> 
      </div>
    </nav>

    <!-- Loader -->
    <div class="is-loading-bar has-text-centered"  v-bind:class="{'is-loading': $store.state.isLoading }">
      <div class="lds-dual-ring"></div>
    </div>

    <section class="section">
      <router-view/>
    </section>

    <!-- Footer Section -->
    <footer class="footer">
      <div class="container">
        <div class="columns is-mobile">
          <div class="column is-12-mobile">
            <router-link to="/" class="navbar-item">
              <i class="fas fa-fire pr-4" style="font-size: 24px; color: orange;"></i>
              <p class="navbar-logo">
                Brique Energy<span class="nav-logo-item">.</span>
              </p>
            </router-link>

            <p>
              Enhancing Every Moment: Premium Products for Grilling & Shisha. Elevate Your Experience with our products!
            </p>
          </div>

          

          <div class="column is-12-mobile">
      <router-link to="/" class="navbar-item">
        <h3>Products</h3>
      </router-link>
      
      <router-link to="/" class="navbar-item">
        <p>New Arrivals</p>
      </router-link>

      <router-link to="/" class="navbar-item">
        <p>On sale</p>
      </router-link>
        
      <router-link to="/" class="navbar-item">
        <p>Top rated</p>
      </router-link>

      <router-link to="/" class="navbar-item">
        <p>Gift Cards</p>
      </router-link>
    </div>

    <div class="column is-12-mobile">
      <router-link to="/" class="navbar-item">
        <h3>Customer Service</h3>
      </router-link>
      
      <router-link to="/" class="navbar-item">
        <p>Contact Us</p>
      </router-link>

      <router-link to="/" class="navbar-item">
        <p>Shipping and Returns</p>
      </router-link>
        
      <router-link to="/" class="navbar-item">
        <p>Privacy Policy</p>
      </router-link>

      <router-link to="/" class="navbar-item">
        <p>Terms and Conditions</p>
      </router-link>
    </div>

    <div class="column is-12-mobile">
      <router-link to="/" class="navbar-item">
        <h3>My Account</h3>
      </router-link>
      
      <router-link to="/" class="navbar-item">
        <p>My Account</p>
      </router-link>

      <router-link to="/" class="navbar-item">
        <p>Order History</p>
      </router-link>
        
      <router-link to="/" class="navbar-item">
        <p>Wish List</p>
      </router-link>

      <router-link to="/" class="navbar-item">
        <p>Newsletter</p>
      </router-link>
    </div>
  </div>
        <hr>

        <div class="navbar-start is-flex">
          <div class="column is-12-mobile">
            <p>
              <i class="fa fa-copyright" aria-hidden="true"></i>
              Copyright@2024
            </p>
          </div>
          
          <div class="navbar-end">
            <!-- Social media icons -->
            <router-link to="/twitter">
              <span class="icon"><i class="fab fa-twitter" style="color: black;"></i></span>
            </router-link>
            
            <router-link to="/instagram">
              <span class="icon"><i class="fab fa-instagram" style="color: black;"></i></span>
            </router-link>
            
            <router-link to="/facebook">
              <span class="icon"><i class="fab fa-facebook" style="color: black;"></i></span>
            </router-link>
          </div>
        </div>
      </div> 
    </footer>
  </div>
</template>


<script>
import { Icon } from '@iconify/vue';

import axios from 'axios'

export default {
  data() {
    return {
      showMobileMenu: false,
      cart: {
        items: []
      }
    };
  },
  beforeCreate() {
    this.$store.commit('initializeStore')

    const token = this.$store.state.token

    if (token) {
      axios.defaults.headers.common['Authorization'] = "Token " + token
    } else {
      axios.defaults.headers.common['Authorization'] = ""
    }
  },
  mounted() {
    this.cart = this.$store.state.cart;
  },
  computed: {
    cartTotalLength() {
      let totalLength = 0

      for (let i = 0; i < this.cart.items.length; i++) {
        totalLength += this.cart.items[i].quantity;
      }

      return totalLength;
    }
  }
};
</script>

<style lang="scss">
@import '../node_modules/bulma';

.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.lds-dual-ring:after {
  content: "";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50px;
  border: 6px solid #ccc;
  border-color: #ccc transparent #ccc transparent;
  animation: lds-dual-ring 1.2s linear infinite;

}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.is-loading-bar {
  height: 0;
  overflow: hidden;

  -webkit-transition: all 0.3s;
  transition: all 0.3s;

  &.is-loading {
    height: 80px;
  }

}

// Navbar
.navbar-logo {
  font-size: 24px; 
  font-weight: 700; 
  color: #333;
}

.nav-logo-item {
  color: orange;
}

/* Optional: Add hover effect to make it more catchy */
.navbar-logo-link:hover .navbar-logo {
  transform: scale(1.1);
  transition: transform 0.3s ease;
}
</style>