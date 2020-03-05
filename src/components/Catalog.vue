<template>
    <div class="shop">
        <ul>
            <li :key="ID" v-for="(product, ID) in products">
                <Product :product="product"></Product>
            </li>
        </ul>
        <h2 v-if="this.products.length === 0">No product available right now!</h2>
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
        padding-right: 250px;
    }

    li {
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    .welcome-message {
    }
</style>
