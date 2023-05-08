<template>
  <h1>{{ name }}</h1>
  <input type="text" v-model="name"><br>
  <button @click="placeOrder">Place Order</button>
  <yummy-meal name="meal.name" :price="meal.price" @addToCart="addItemToCart" />
</template>

<script>
import YummyMeal from "./components/YummyMeal.vue";
import { ref, reactive } from "vue";

export default {
  components: { YummyMeal },

  setup() {
    const name = ref("The Snazzy Burger");
    name.value = "Hello from the setup function";

    const meal = reactive({ name: "Hamburger", price: 5});

    console.log(meal.name);

    const placeOrder = () => alert("Yut order 2 has been placed !");
    const addItemToCart = (item) => alert(`Le produit ${item} a bien été ajouté au panier`);

    return {name, meal, placeOrder, addItemToCart};
  },

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
