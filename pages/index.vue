<template>
<div class="container">
<div class="row">
<Card
 v-for="(product, index) in products"
          :key="index"
          :product="product"
          @addToCart ="updateCart"
/>
  <div class="cart">Cart({{ cart.length }})</div>
</div>
</div>
</template>
<script>
import Card from '@/components/Card.vue'
    export default {
      data() {
        return {
          cart:[],
          title: 'Products'
        }
      },
      asyncData({ $axios }) {
        return $axios.get('http://localhost:3000/products').then(response => {
          return {
            products: response.data
          }
        }).catch(e => {
error({statusCode: 503, message: 'Unable to fetch products at this time, please try again'})
})
      },
      components: {
        Card
      },
methods: {
updateCart() {
this.cart += 1
}
}
  }

    </script>
