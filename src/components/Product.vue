<template>
    <div class="product">
        <div class="product-image">
            <img :src="image" alt="product image">
        </div>

        <div class="product-info">
            <h2>{{ name }}</h2>
            <div v-if="inStock">
                <p>In Stock</p>
                <p>Price: ${{price}}.00</p>
            </div>
            <p v-else>Out of Stock</p>

            <p>Most described in our reviews as:</p>
            <ul>
                <li :key="index" v-for="(detail, index) in details">{{ detail }}</li>
            </ul>

            <button :class="{ disabledButton: !inStock, activeAdd: inStock }"
                    :disabled="!inStock"
                    @click="addToCart"
            >
                Add to cart
            </button>

        </div>
    </div>
</template>

<script>
    import EventBus from "@/shared/EventBus";

    export default {
        name: "Product",
        props: {
            product: {
                type: Object,
                required: false
            }
        },
        methods: {
            addToCart() {
                EventBus.$emit('add-to-cart', this.ID);
            }
        },
        computed: {
            image() {
                return this.product.image;
            },
            ID() {
                return this.product.ID;
            },
            details() {
                return this.product.details;
            },
            inStock() {
                return this.product.quantity > 0;
            },
            name() {
                return this.product.brand + "'s " + this.product.name;
            },
            price() {
                return this.product.price;
            }
        }
    }
</script>

<style scoped>
    .product {
        display: flex;
        flex-flow: wrap;
        padding: 1rem;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    img {
        border: 1px solid #d8d8d8;
        width: 70%;
        margin: 40px;
        box-shadow: 0 1px 1px #d8d8d8;
    }

    .product-image {
        max-width: 700px;
    }

    .product-image {
        margin-top: 10px;
        width: 50%;
    }

    .product-info {
        margin-top: 10px;
        width: auto;
    }

    button {
        margin-top: 30px;
        border: none;
        background-color: #1E95EA;
        color: white;
        height: 40px;
        width: fit-content;
        font-size: 14px;
        margin-left: 15px;
        border-radius: 10%;
    }

    .activeAdd {
        background-color: #1E95EA;
        cursor: pointer;
    }

    .disabledButton {
        background-color: #d8d8d8;
    }
</style>