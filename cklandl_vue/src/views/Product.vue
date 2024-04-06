<template>

    <div class="page-product">
        <div class="columns is-multiline">
            <div class="column is-6">
                <figure class="image mb-6">
                    <img v-bind:src="product.get_image" style="border-radius: 16px;">
                </figure>
            </div>

            <div class="column is-6 is-flex is-flex-direction-column is-justify-content-center">
                <h2 class="subtitle">Information</h2>

                <div class="is-flex is-justify-content-space-between is-align-items-center">
                    <h1 class="title">{{ product.name }}</h1>

                    <p class="subtitle">${{ product.price }}</p>

                </div>

                <p>{{ product.description }}</p>

                <hr>

                <div class="field has-addons mt-6 mb-6 ">
                    <div class="control pr-4">
                        <input type="number" class="input" min="1" v-model="quantity">
                    </div>

                    <div class="control">
                        <a href="" class="button is-dark" @click="addToCart">Add to cart</a>
                    </div>
                </div>

                <hr>

                <div class="is-flex">
                    <div class="navbar-item">
                        <router-link to="/cart" class="nav-button is-flex">
                            <span class="icon"><i class="far fa-heart" style="color: black;"></i></span>
                            <span><p>Add to wishlist</p></span>
                        </router-link>
                    </div>

                    <div class="navbar-item">
                        <router-link to="/cart" class="nav-button is-flex">
                            <span class="icon"><i class="far fa-share-alt" style="color: black;"></i></span>
                            <span><p>Share</p></span>
                        </router-link>
                    </div>
                </div>
            </div>

        </div>

    </div>
</template>

<script>
import axios from 'axios'
import { toast } from 'bulma-toast'

export default {
    name: 'Product',
    data() {
        return {
            product: {},
            quantity: 1
        }
    },
    mounted() {
        this.getProduct()
    },
    methods: {
        async getProduct() {
            this.$store.commit('setIsLoading', true)

            const category_slug = this.$route.params.category_slug
            const product_slug = this.$route.params.product_slug

            await axios
            .get(`/api/v1/products/${category_slug}/${product_slug}`)
            .then(response => {
                this.product = response.data

                document.title = this.product.name + '| CKLove&Light'
            })
            .catch(error => {
                console.log(error)
            })

            this.$store.commit('setIsLoading', false)
        },
        addToCart() {
            console.log('addToCart')
            if (isNaN(this.quantity) || this.quantity < 1) {
                this.quantity = 1
            }


            const item = {
                product: this.product,
                quantity: this.quantity
            }

            this.$store.commit('addToCart', item)

            toast({
                message: 'The product was added to the cart',
                type: 'is-success',
                dismissible: true,
                pauseOnHover: true,
                duraton: 2000,
                position: 'bottom-right'
            })
        }
    }
}
</script>

<style>

</style>