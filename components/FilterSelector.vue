<template>
  <div>
    <!-- This component chooses what we selecting by -->
    <button
      class="border rounded p-4 m-1"
      v-for="l in letters"
      :key="l"
      @click="setLetter(l)"
    >
        {{ l }}
    </button>
    <div>
      selectedLetter: <b>{{ theLetter }}</b>
    </div>
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
    setLetter(l){
      this.$store.commit('SET_LETTER', l)
    }
  },

  computed: {
    theLetter() {
      return this.$store.state.selectedLetter
    }
  }
}
</script>

<style scoped>
button {
  font-family: monospace;
}
</style>
