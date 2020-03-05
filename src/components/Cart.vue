<template>
    <div class="cart-section">
        <div class="cart" @click="toggleCart">
            <p>Cart({{ total }})</p>
        </div>
        <div class="cart-detail" v-show="isOpen">
            <ul>
                <li v-for="(value, key) in items" :key="key">
                    <div class="product">
                        <div class="product-image">
                            <img :src="products[key].image" alt="product image">
                        </div>

                        <div class="product-info">
                            <h2>{{ products[key].name }}</h2>
                            <p>Quantity: {{value}}</p>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
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
            return{
                items: {},
                isOpen: false
            }
        },
        methods: {
          toggleCart(){
              this.isOpen = !this.isOpen;
          }
        },
        computed: {
            total(){
                return Object.keys(this.items).reduce((sum,key)=>sum+parseInt(this.items[key]||0),0).toString();
            }
        },
        mounted() {
            EventBus.$on('add-to-cart', productID => {
                if (Object.keys(this.items).includes(productID))
                {
                    let value = this.items[productID];
                    this.$set(this.items, productID, ++value);
                }
                else
                {
                    this.$set(this.items, productID, 1);
                }
            });
            EventBus.$on('remove-from-cart', productID => {
                if (this.items[productID] > 1)
                {
                    let value = this.items[productID];
                    this.$set(this.items, productID, --value);
                }
                else
                {
                    this.$delete(this.items, productID);
                }
            });
        }
    }
</script>

<style scoped>
.cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
}
.product-image{
    margin-top: 10px;
    width: 50%;
}

.product-info {
    margin-top: 10px;
    width: 20%;
}
</style>