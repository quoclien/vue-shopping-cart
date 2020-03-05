<template>
    <div class="product">
        <div class="product-image">
            <img :src="image" alt="product image">
        </div>

        <div class="product-info">
            <h2>{{ name }}</h2>
            <p v-if="inStock">In Stock</p>
            <p v-else>Out of Stock</p>

            <ul>
                <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
            </ul>

            <button @click="addToCart"
                    :disabled="!inStock"
                    :class="{ disabledButton: !inStock, activeAdd: inStock }"
            >
                Add to cart
            </button>
            <button @click="removeFromCart"
                    :disabled="!inCart"
                    :class="{ disabledButton: !inCart, activeRemove: inCart }"
            >
                Remove from cart
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
        data: function () {
            return{
                addedNumber: 0
            }
        },
        methods: {
          addToCart(){
              EventBus.$emit('add-to-cart', this.ID);
              this.addedNumber++;
          },
            removeFromCart(){
              EventBus.$emit('remove-from-cart', this.ID);
              this.addedNumber--;
            }
        },
        computed: {
            image(){
                return this.product.image;
            },
            ID(){
                return this.product.ID;
            },
            details(){
                return this.product.details;
            },
            inStock(){
                return (this.product.quantity - this.addedNumber) > 0;
            },
            inCart(){
                return this.addedNumber > 0;
            },
            name(){
                return this.product.brand + "'s " + this.product.name;
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

    ul{
        text-align: start;
    }

    img {
        border: 1px solid #d8d8d8;
        width: 70%;
        margin: 40px;
        box-shadow: 0 1px 1px #d8d8d8;
    }

    .product-image {
        width: 80%;
    }

    .product-image{
        margin-top: 10px;
        width: 50%;
    }

    .product-info {
        margin-top: 10px;
        width: 20%;
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

    .activeRemove{
        background-color: brown;
        cursor: pointer;
    }

    .activeAdd{
        background-color: #1E95EA;
        cursor: pointer;
    }

    .disabledButton {
        background-color: #d8d8d8;
    }
</style>