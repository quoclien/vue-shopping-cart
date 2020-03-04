<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
    <NavbarHeader site="AmaVue"></NavbarHeader>
      <Cart :products="products"></Cart>
    <Catalog msg="Check those awesome products below!" :products="this.products"/>
  </div>
</template>

<script>
import Catalog from './components/Catalog.vue'
import NavbarHeader from "@/components/NavbarHeader";
import Cart from "@/components/Cart";
import kindle from "@/assets/amazonKindleOasis.png";
import iphone from "@/assets/iphone11ProMax.png";
import sony from "@/assets/sonyAlphaA7.png";

export default {
  name: 'App',
  components: {
      Cart,
    Catalog,
    NavbarHeader
  },
    data: function () {
        return{
            products: {
                s1:
                    {
                    ID: "s1",
                    image: kindle,
                    name: "Kindle Oasis",
                    brand: "Amazon",
                    details: ["Useful", "Durable", "Light-weight"],
                    quantity: 3
                    },
                s2:
                {
                    ID: "s2",
                    image: iphone,
                    name: "iPhone 11 Pro Max",
                    brand: "Apple",
                    details: ["Expensive", "Luxurious", "Apple's"],
                    quantity: 10
                },
                s3:
                {
                    ID: "s3",
                    image: sony,
                    name: "Alpha A7 R III",
                    brand: "Sony",
                    details: ["Modern", "Functional", "Fast"],
                    quantity: 0
                }
            }
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
