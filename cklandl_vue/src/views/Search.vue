<template>
    <div class="page-search">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title is-bold">Shop</h1>

                <div class="navbar-start">
                    <div class="navbar-item">
                        <form method="get" action="/search">
                            <div class="field has-addons">
                                <div class="control">
                                    <input type="text" class="input" placeholder="Search here" name="query">
                                </div>
                                <div class="control">
                                    <button class="button is-black">
                                        <span class="icon">
                                            <i class="fas fa-search"></i>
                                        </span>
                                    </button>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>

                <h2 class="is-size-5 has-text-grey">Search term: "{{ query }}"</h2>

            </div>

            <ProductBox
                v-for="product in products"
                v-bind:key="product.id"
                v-bind:product="product"
            />
        </div>
        

        <h1 class="title is-bold mb-6">Our Products</h1>
        <div class="columns is-multiline">
            <ProductBox
            v-for="product in latestProducts"
            v-bind:key="product.id"
            v-bind:product="product"/>
        </div>

        <div class="columns is-multiline">
            <ProductBox
            v-for="product in latestProducts"
            v-bind:key="product.id"
            v-bind:product="product"/>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

import ProductBox from '@/components/ProductBox';
export default {
    name: 'Search',
    components: {
        ProductBox
    },
    data() {
        return {
            products: [],
            query: '',
            latestProducts: [],
        }
    },
    mounted() {
        this.getLatestProducts()

        document.title = 'Search | CKLove&Light'

        let uri = window.location.search.substring(1)
        let params = new URLSearchParams(uri)

        if (params.get('query')) {
            this.query = params.get('query')

            this.performSearch()
        }
    },
    methods: {
        async performSearch() {
            this.$store.commit('setIsLoading', true)

            await axios
            .post('/api/v1/products/search/', {'query': this.query})
            .then(response => {
                this.products = response.data
            })
            .catch(error => {
                console.log(error)
            })

            this.$store.commit('setIsLoading', false)
        },

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

<style>

</style>