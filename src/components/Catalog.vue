<template>
  <div class="hello">
    <h2>{{ msg }}</h2>
    <ul>
      <li v-for="product in products" :key="product.ID">
        <Product :product="product"></Product>
      </li>
    </ul>
  </div>
</template>

<script>
import Product from "@/components/Product";
import iphone from '../assets/iphone11ProMax.png';
import kindle from '../assets/amazonKindleOasis.png';
import sony from '../assets/sonyAlphaA7.png';
export default {
  name: 'HelloWorld',
  components: {Product},
  props: {
    msg: String
  },
  data: function () {
    return{
      products: [
        {
          ID: "s1",
          image: kindle,
          name: "Kindle Oasis",
          brand: "Amazon",
          details: ["Useful", "Durable", "Light-weight"],
          quantity: 3
        },
        {
          ID: "s2",
          image: iphone,
          name: "iPhone 11 Pro Max",
          brand: "Apple",
          details: ["Expensive", "Luxurious", "Apple's"],
          quantity: 10
        },
        {
          ID: "s3",
          image: sony,
          name: "Alpha A7 R III",
          brand: "Sony",
          details: ["Modern", "Functional", "Fast"],
          quantity: 0
        }
      ]
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
