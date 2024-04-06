<template>

<section class="hero mb-6 is-flex is-flex-direction-row">

<!-- Right half -->
<div class="column is-half is-flex is-justify-content-center is-hidden-mobile">
  <img src="../assets/contact-us.jpg" alt="Image" style="border-radius: 16px;">
</div>
<!-- Left half -->
<div class="column is-half is-flex is-justify-content-center is-align-items-center">
  <div>
    <p class="title mb-4 is-size-2">
      Talk To Us
    </p>
    <p class="mb-6">
        Got questions or feedback? We're here to help! Reach out to us via phone, email, or simply drop by our store. Our dedicated team is ready to assist you with any inquiries, provide expert advice, or address any concerns you may have. Your satisfaction is our priority, and we look forward to hearing from you soon!
    </p>
  </div>
</div>
</section>

    <div>
        <p class="title mb-6 is-size-2">
            Send Us a Message
        </p>
        <form @submit.prevent="submitForm" class="box">
            <div class="field">
                <label class="label">Name</label>
                <div class="control">
                    <input type="text" name="name" v-model="name" class="input">
                </div>
            </div>
            
            <div class="field">
                <label class="label">Email</label>
                <div class="control">
                    <input type="email" name="email" v-model="email" class="input">
                </div>
            </div>
            <div class="field">
                <label class="label">Message</label>
                <div class="control">
                    <textarea name="message" v-model="message" class="textarea"></textarea>
                </div>
            </div>
            <div class="field">
                <div class="control">
                    <button type="submit" class="button is-black">Send Message</button>
                </div>
            </div>
        </form>
    </div>
  </template>

  <script>
  const WEB3FORMS_ACCESS_KEY = "8a7c318d-d0ff-4edc-b868-31c84e032b3a";

  export default {
    name: 'ContactPage',
    data() {
      return {
        name: "",
        email: "",
        message: "",
      };
    },
    methods: {
      async submitForm() {
        const response = await fetch("https://api.web3forms.com/submit", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
          body: JSON.stringify({
            access_key: WEB3FORMS_ACCESS_KEY,
            name: this.name,
            email: this.email,
            message: this.message,
          }),
        });
        const result = await response.json();
        if (result.success) {
          console.log(result);
        }
      },
    },
  };
  </script>