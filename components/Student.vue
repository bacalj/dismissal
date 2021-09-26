<template>
  <div v-show="amInFilter" class="rounded shadow p-3 bg-white mb-2 flex justify-betweeen">
    <div class="name w-1/3">{{ first }} {{ last }}</div>
    <div class="room w-1/6">{{ room }}</div>
    <div class="status w-1/2">{{ status }}</div>
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

