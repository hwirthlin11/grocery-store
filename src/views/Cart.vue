<template>
<div>
<h1> Your Cart: </h1>
  <h2 v-if = "this.$root.$data.cart.length < 1"> Oh no! Your cart is empty. </h2>
  <div v-for="result in filteredArray" :key="result.name">
    {{ result.count }} {{ result.name }}
  </div>
  <div class="cart">
    <div class="cartItem" v-for="item in cart" :key="item.id">
      <div class="info">
        <img :src="'/images/products/'+item.image">
        <h3>{{item.name}}</h3>
        <p>{{item.price}}</p>
        <button class="removeButton" v-on:click = 'remove(item)'>Remove!</button>
      </div>
    </div>
  </div>
</div>
</template>
<script>
export default {
  name: 'Cart',
  props: {
    carts: Array
  },
  components: {

  },
  data() {
    return {

    }
  },
  computed: {
    cart() {
      return this.$root.$data.cart;
    },
    filteredArray() {
      return this.count(this.$root.$data.cart);
    }
  },
  methods: {
    remove(item){
      this.$root.$data.cart.splice(this.$root.$data.cart.indexOf(item), 1);
    },
  count(array) {
  //add 1 if the color exists, initialize as 1 if it does not
  let counts = array.reduce((out, {name}) => ({ ...out, [name]: out[name]+1 || 1}), {});
  return Object.keys(counts).map(key => ({name: key, count: counts[key]}));
}
  }
}
</script>
<style>
  div {
    text-align: center;
  }
  .cart {
    margin-left:400px;
  }
  .removeButton {
    height: 50px;
    background: #000;
    color: white;
    border: none;
    margin-bottom: 30px;
  }
  .cartItem{
    border: 3px solid black;
    margin: 30px;
    width: 350px;
    background-color: #f8edeb;
  }
  img{
    padding-top:50px;
  }
</style>
