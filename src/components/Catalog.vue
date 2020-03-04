<template>
  <div class="hello">
    <h2>{{ msg }}</h2>
    <ul>
      <li v-for="product in products" :key="product.ID">
        <Product :product="product"></Product>
      </li>
    </ul>
    <h3 v-if="this.products.length === 0">No product available right now!</h3>
  </div>
</template>

<script>
import Product from "@/components/Product";
export default {
  name: 'Catalog',
  components: {Product},
  props: {
    msg: String,
    products: {
      type: Object,
      required: false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
