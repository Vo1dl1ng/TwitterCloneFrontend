<template>
<div>
    <div>
        <ul>
            <li v-for="Product in Products" :key="Product.id">
                <Product :product="Product"/>
                <button @click="buy(Product)">Buy</button>
            </li>
        </ul>
    </div>
</div>
</template>

<script>
import Product from './product/Product.vue'

export default {
 components: {
     Product,
 },

 props: ['Products'],

 methods: {
     buy(product) {
         this.$emit('addToCart', product)
     }
 }
}
</script>

<style scoped>
</style>