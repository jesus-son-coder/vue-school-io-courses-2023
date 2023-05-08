<template>
  <h1>{{ name }}</h1>
  <input type="text" v-model="name"><br>
  <button @click="placeOrder">Place Order</button>
  <yummy-meal name="Hamburger" :price="Number(5)" @addToCart="addItemToCart" />
</template>

<script>
import YummyMeal from "./components/YummyMeal.vue";
import { ref } from "vue";

export default {
  components: { YummyMeal },
  setup() {
    const name = ref("The Snazzy Burger");

    console.log(name.value);

    function placeOrder() {
      this.name = "KFC Burger ;)"
      alert(`${this.name}: your order has been placed`);
    }
    // Utilisation de la syntaxe raccourcie :
    const placeOrder2 = () => alert("Yut order 2 has been placed !");

    const addItemToCart = (item) => alert(`Le produit ${item} a bien été ajouté au panier`);

    return {name, placeOrder, placeOrder2, addItemToCart};
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
  margin-top: 60px;
}
</style>
