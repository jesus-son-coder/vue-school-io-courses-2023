<template>
  <div>
    <p>
      <strong>{{ name }}</strong>
      {{ pricePrettySentence }}
    </p>
    <button @click="addToCart">Add to Cart</button>
  </div>

</template>

<script>
import { computed } from 'vue';
export default {
  props: {
    name: String,
    price: Number,
  },
  setup(props, { emit }) {
    const addToCart = () => emit('addToCart', props.name);
    const pricePretty = computed(() => `$${props.price.toFixed(2)}`);

    const pricePrettySentence = computed(
      () => `The price of this is ${pricePretty.value}`
    );

    return { addToCart, pricePretty, pricePrettySentence };
  },

}
</script>

<style>
</style>
