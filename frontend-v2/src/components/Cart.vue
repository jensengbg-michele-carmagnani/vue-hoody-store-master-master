<template>
  <aside id="cart">
      <div class="cart-icon" @click="toggleCart"></div>
      <section class="cart-items" v-if="showCart">
          <article class="item" v-for="(item, index) in cart" :key="index" >{{ item.name }}</article>
          <p class="total">total cost: <b>{{ totalCost }}:-</b></p>
          <a href="#" class="btn" @click.prevent="sendOrder">Buy it!</a>
      </section>
  </aside>
</template>

<script>
export default {
    name: 'Cart',
    methods: {
        toggleCart(){
           this.$store.commit('toggleCart');
        },
        sendOrder(){
            this.$store.dispatch('sendOrder');
        }
    },
    computed: {
        cart(){
            return this.$store.state.cart;
        },
        totalCost(){
            return this.$store.state.cart.reduce((acc, item) => acc + item.price, 0)
        },
        showCart(){
            return this.$store.state.ui.showCart;
        }
    }
}
</script>

<style lang="scss">

@import './../scss/variables';

#cart {
    position: relative;
    width: 240px;

    .cart-icon {
        width: 3rem;
        height: 3rem;
        background: red;
        margin-left: auto;
        border-radius: 999rem;
    }

    .cart-items {
        position: absolute;
        top: 120%;
        background: white;
        padding: 1rem;
        box-sizing: border-box;
        width: 100%;
        box-shadow: $boxShadow;

        .btn {
            margin: 2rem 0 0 0;
            max-width: 100%;
        }

    }
}

</style>