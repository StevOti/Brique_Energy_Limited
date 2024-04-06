<template>
  <div class="about">
    
      <section class="hero mb-6 is-flex">

        <!-- Right half -->
        <div class="column is-half is-flex is-justify-content-center">
          <img src="../assets/business-team-working-reports.jpg" alt="Image" style="border-radius: 16px;">
        </div>
        <!-- Left half -->
        <div class="column is-half is-flex is-justify-content-center is-align-items-center">
          <div>
            <p class="title mb-4 is-size-2">
              ABOUT US
            </p>
            <p class="mb-6">
              At Brique Energy, we're passionate about providing high-quality briquettes and shisha charcoal to enhance your grilling and smoking experiences. With a commitment to sustainability and excellence, we strive to deliver innovative products that elevate every moment, whether you're a seasoned grill master or a shisha enthusiast. Discover our story and join us on our journey to redefine the art of outdoor cooking and relaxation.
            </p>
            
            <router-link to="/search" class="buttons">
              <a href="#" class="button is-black">Contact Us</a>
            </router-link>
          </div>
        </div>
      </section>

      <section class="hero mb-6 is-flex">  
        <!-- Left half -->
        <div class="column is-half is-flex is-justify-content-center is-align-items-center">
          <div>
            <p class="title mb-4 is-size-2">
              What We Do
            </p>
            
            <p class="mb-6">
              We pride ourselves on our dedication to crafting exceptional briquettes and shisha charcoal that elevate every aspect of your grilling, smoking, and cooking endeavors. Our range of products is meticulously designed and manufactured to deliver superior performance, consistency, and flavor enhancement. With a focus on sustainability and environmental responsibility, we source only the finest raw materials and employ innovative production techniques to minimize waste and maximize efficiency. Whether you're a seasoned grill master, a shisha enthusiast, or a culinary enthusiast exploring new horizons, we're here to provide you with the highest quality products and unparalleled customer service. Join us in our mission to revolutionize the way you experience outdoor cooking and relaxation.
            </p>
            
            <router-link to="/search" class="buttons">
              <a href="#" class="button is-black">Check Latest Products</a>
            </router-link>
          </div>
        </div>

        <!-- Right half -->
        <div class="column is-half is-flex is-justify-content-center">
          <img src="../assets/workers.jpg" alt="Image" style="border-radius: 16px;">
        </div>
      </section>
    
  </div>
</template>

<script>
export default {
  name: 'AboutPage',
  data() {
    return {
    };
  },
  methods: {
  },
};
</script>

<style scoped>
@media screen and (min-width: 769px) {
  .hero {
    flex-direction: row;
  }
  .column.is-half {
    width: 50%;
  }
  .column.is-half:first-child {
    align-items: center;
  }
}
</style>