<template>
<div>
  <div>
        <img :src="product.image" alt="product.title">
        <h2>{{product.title}}</h2>
        <h3>{{product.price}}</h3>
        {{product.category}} |
        {{product.description}} |
        {{product.id}} |
        {{product.rating}} |
        <p><br></p>
  </div>
</div>
</template>

<script>
export default {
    props: ['product']
}
</script>

<style scoped>
    img {
        max-height: 100px;
    }
</style>