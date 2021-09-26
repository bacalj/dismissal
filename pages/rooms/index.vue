<template>
  <div class="py-12 px-6">

    <nuxt-link v-for="c in classim" :key="c" :to="/rooms/ + c">{{ c }}</nuxt-link>

  </div>
</template>

<script>
export default {
  data(){
    return {
      classim: [
        'KT', 'KL', '1M', '2W', '3Z', '3N', '4A', '4E', '5M', '5D', '6K', '6G'
      ]
    }
  }
}
</script>
<style lang="postcss" scoped>
a {
  @apply px-3 py-2 rounded border border-gray-200 bg-white p-12 shadow rounded m-2;
  display: inline-block;
}

a:hover {
  @apply bg-green-200 border-green-200
}
</style>
