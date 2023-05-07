<template>
  <div>
    <h1>Most Popular Rivers in the World</h1>
    <ul>
      <li v-for="(river, index) in rivers" :key="`$river-${index}`">
        <a :href="river.image" target="_blank">{{ river.title }}</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',

  head: {
    meta: [
      {
        hid: 'title',
        content: 'Home Page RV CK'
      },
      {
        hid: 'description',
        content: 'This is the Home Page of RV CK'
      },
    ]
  },

  data() {
    return {
      rivers: []
    }
  },

  async asyncData ({ $http }) {
    const res = await $http.$get('https://api.nuxtjs.dev/rivers');
    return {
      rivers: res
    }
  }

  /*
    async fetch () {
      const res = await this.$http.$get('https://api.nuxtjs.dev/rivers');
      this.rivers = res;
    }
   */
}
</script>
