<template>
  <div>
    <!-- This component chooses what we selecting by -->
    <div class="name-buttons p-2 rounded mb-4">
      <h2>Show List by First Letter of Last Name</h2>

      <button
        class="border rounded px-6 py-1 m-1"
        v-for="l in letters"
        :key="l"
        @click="selecta(l)"
        :class="{ litUp: $store.state.selectado == l }"
      >
          {{ l }}
      </button>
    </div>

    <div class="class-buttons p-2 rounded">
      <h2>Show list by classroom</h2>

      <button
        class="border rounded px-6 py-1 m-1"
        v-for="c in classes"
        :key="c"
        @click="selecta(c)"
        :class="{ litUp: $store.state.selectado == c }"
      >
          {{ c }}
      </button>
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
    selecta(algo){
      this.$store.commit('SELECTA', algo)
    }
  }
}
</script>

<style scoped>
button {
  font-family: monospace;
  border-color: #333;
  background-color:white;
}

button.litUp {
  background-color: lightgreen;
}
</style>
