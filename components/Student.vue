<template>
  <div v-show="amInFilter">
    {{ first }} {{ last }} | {{ room }} <em>{{ status }}</em> <br>
    <pre><code>{{ this.$store.state.selectado }}</code></pre>
  </div>
</template>

<script>


export default {

  watch: {
    status(val, oldVal) {
      console.log(val, oldVal);
    },
  },

  computed: {
    amInFilter(){
      if ( this.$store.state.selectado == null){
        return true
      }

      else {
        if (this.room == this.$store.state.selectado){
          return true
        }

        else if (this.last.substring(0,1).toLowerCase() == this.$store.state.selectado){
          return true
        }

        else {
          return false
        }
      }
    }
  },

  props: {
    first: String,
    last: String,
    room: String,
    status: String
  }
}
</script>

