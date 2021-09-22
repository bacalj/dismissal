<template>
  <div>
    <!-- This component chooses what we selecting by -->
    <button
      class="border rounded px-6 py-1 m-1"
      v-for="l in letters"
      :key="l"
      @click="selecta(l)"
    >
        {{ l }}
    </button>

    <hr class="my-6">

    <button
      class="border rounded px-6 py-1 m-1"
      v-for="c in classes"
      :key="c"
      @click="selecta(c)"
    >
        {{ c }}
    </button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      letters: [
        'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'
      ],
      classes: [
        'KT', 'KL', '1M', '2W', '3Z', '3N', '4A', '4E', '5M', '5D', '6K', '6G'
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
  font-family: monospace;
}
</style>
