<template>
  <div v-show="amInFilter" class="rounded shadow p-3 bg-white mb-2 flex justify-betweeen">
    <div class="name w-1/3">{{ first }} {{ last }}</div>
    <div class="room w-1/6">{{ room }}</div>
    <div class="status-radio w-1/2">

      <input type="radio" id="waiting" value="waiting" v-model="status">
      <label for="Walking">waiting</label>

      <input type="radio" id="dismissed" value="dismissed" v-model="status">
      <label for="two">Dismissed</label>

      <span class="ml-3">Status: {{ status }}</span>
    </div>
  </div>
</template>

<script>


export default {
  /* ok gotta do this right vis-a-vis firebase magic, vue magic, etc.
  vue.runtime.esm.js?2b0e:619 [Vue warn]: Avoid mutating a prop directly since the value will be overwritten whenever the parent component re-renders. Instead, use a data or computed property based on the prop's value. Prop being mutated: "status"
  */
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

