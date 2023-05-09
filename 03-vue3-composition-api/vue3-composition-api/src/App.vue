<template>
  <h1>{{ name }}</h1>
  <input type="text" v-model="name"><br>
  <button @click="placeOrder">Place Order</button>
  <yummy-meal :name="meal.name" :price="meal.price" @addToCart="addItemToCart" />
</template>

<script>
import YummyMeal from "./components/YummyMeal.vue";
import { ref, reactive } from "vue";

export default {
  components: { YummyMeal },

  setup() {
    const name = ref("The Snazzy Burger");
    const meal = reactive({ name: "Hamburger", price: 5});

    const placeOrder = () => alert("Yut order 2 has been placed !");
    const addItemToCart = (item) => alert(`Le produit ${item} a bien été ajouté au panier`);

    let posts = ref(['post 1', 'post 2']);
    posts.value = ['post 3', 'post 4'];



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
