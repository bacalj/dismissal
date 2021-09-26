<template>
  <div>
    <!-- This component chooses what we selecting by -->
    <div class="name-buttons p-2 mb-4 bg-gray-300">
      <button
        class="border rounded px-6 py-1 m-1"
        v-for="l in letters"
        :key="l"
        @click="selecta(l)"
        :class="{ litUp: $store.state.selectado == l }"
      >
          {{ l.toUpperCase() }}
      </button>

      <button class="border rounded px-6 show-all py-1 m-1" @click="showAll">Show All</button>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      letters: [
        'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'
      ]
    }
  },

  methods: {
    selecta(algo){
      this.$store.commit('SELECTA', algo)
    }
  }
}
</script>

<style scoped>
button {
  @apply bg-white border-none m-2;
  width:60px;
}

button.show-all {
  width:auto;
  @apply bg-indigo-100;
}

button.litUp {
  @apply bg-red-100;
}
</style>
