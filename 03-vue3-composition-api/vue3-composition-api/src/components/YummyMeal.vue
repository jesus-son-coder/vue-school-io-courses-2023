<template>
  <div>
    <p>
      <strong>{{ name }}</strong>
      {{ price }}€
    </p>
    <button @click="addToCart">Add to Cart</button>
  </div>

</template>

<script>
export default {
  props: {
    name: String,
    price: Number,
  },
  setup(props, { attrs, emit, slots}) {
    const addToCart = () => emit('addToCart', props.name);
    return { addToCart };
  }
}
</script>

<style>
</style>
