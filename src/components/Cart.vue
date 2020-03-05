<template>
    <div class="cart-section">
        <div @click="toggleCart" class="cart">
            <p>Cart({{ number }})</p>
        </div>
        <div class="cart-detail" v-show="isOpen">
            <ul>
                <li :key="key" v-for="(value, key) in items">
                    <div class="product">
                        <div class="product-image">
                            <img :src="products[key].image" alt="product image">
                        </div>

                        <div class="product-info">
                            <h2>{{ products[key].name }}</h2>
                            <p>Quantity: {{value}}</p>
                            <p>Subtotal: ${{parseInt(value) * parseInt(products[key].price)}}.00</p>
                            <button :class="{ disabledButton: !value, activeRemove: value }"
                                    :disabled="!value"
                                    @click="removeFromCart(key)"
                            >
                                Remove from cart
                            </button>
                        </div>
                    </div>
                </li>
            </ul>
            <p>Total: ${{total}}.00</p>
        </div>

        <button :class="{ disabledButton: !Object.keys(items).length, activeCheckOut: Object.keys(items).length }"
                :disabled="!Object.keys(items).length"
                @click="checkOut"
                v-show="isOpen"
        >
            Checkout
        </button>
    </div>
</template>

<script>
    import EventBus from "@/shared/EventBus";

    export default {
        name: "Cart",
        props: {
            products: {
                type: Object,
                required: false
            }
        },
        data: function () {
            return {
                items: {},
                isOpen: false
            }
        },
        methods: {
            toggleCart() {
                this.isOpen = !this.isOpen;
            },
            removeFromCart(ID) {
                EventBus.$emit('remove-from-cart', ID);
            },
            checkOut() {
                for (let key in this.items) {
                    this.$delete(this.items, key);
                }
            }
        },
        computed: {
            number() {
                return Object.keys(this.items).reduce((sum, key) => sum + parseInt(this.items[key] || 0), 0);
            },
            total() {
                return Object.keys(this.items).reduce((sum, key) => sum + (parseInt(this.products[key].price) * parseInt(this.items[key]) || 0), 0);
            }
        },
        mounted() {
            EventBus.$on('add-to-cart', productID => {
                if (Object.keys(this.items).includes(productID)) {
                    let value = this.items[productID];
                    this.$set(this.items, productID, ++value);
                } else {
                    this.$set(this.items, productID, 1);
                }
            });
            EventBus.$on('remove-from-cart', productID => {
                if (this.items[productID] > 1) {
                    let value = this.items[productID];
                    this.$set(this.items, productID, --value);
                } else {
                    this.$delete(this.items, productID);
                }
            });
        }
    }
</script>

<style scoped>
    ul {
        list-style-type: none;
        padding: 0;
    }

    img {
        max-width: 100%;
    }

    .cart-section {
        margin-right: 5px;
        float: right;
        border: 1px solid #d8d8d8;
        padding: 5px 20px;
    }

    .cart {
        cursor: pointer;
    }

    .product-image {
        margin-top: 10px;
        width: 200px;
    }

    .product-info {
        margin-top: 10px;
    }

    .activeRemove {
        background-color: brown;
        cursor: pointer;
    }

    .disabledButton {
        background-color: #d8d8d8;
    }

    .activeCheckOut {
        background-color: ghostwhite;
        color: #282828;
        cursor: pointer;
        font-size: large;
    }

    button {
        font-size: medium;
        border: 1px solid black;
        border-radius: 10%;
    }
</style>