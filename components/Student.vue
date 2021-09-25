<template>
  <div v-show="amInFilter()">
    {{ first }} {{ last }} | {{ inClass }} <em>{{ status }}</em>
  </div>
</template>

<script>


export default {

  watch: {
    status(val, oldVal) {
      console.log(val, oldVal);
    },
  },

  methods: {
    amInFilter(){
      if ( this.$store.state.selectado == null){
        return true
      }

      else {
        if (this.inClass == this.$store.state.selectado){
          return true
        }

        else if (this.last.substring(0,1) == this.$store.state.selectado){
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
    inClass: String,
    status: String
  }
}
</script>

