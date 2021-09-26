<template>
  <div v-show="amInFilter" class="rounded shadow p-3 bg-white mb-2 flex justify-betweeen">
    <div class="name w-1/3">{{ first }} {{ last }}</div>
    <div class="room w-1/6">{{ room }}</div>
    <div class="status-radio w-1/2">

      <input type="radio" id="waiting" value="waiting" v-model="localStatus">
      <label for="Walking">Waiting</label>

      <input type="radio" id="dismissed" value="dismissed" v-model="localStatus">
      <label for="two">Dismissed</label>

      <pre class="bg-gray-200">
        <code>this.localStatus: {{ localStatus }}</code>
        <code>this.status: {{ status }}</code>
      </pre>

    </div>
  </div>
</template>

<script>


export default {

  watch: {
    localStatus(val, oldVal) {
      console.log("send an event up to change ", this.studentId, " from ", oldVal, " to ", val, );
    },
  },

  data(){
    return {
      localStatus: null
    }
  },

  mounted(){
    this.setLocalStatus()
  },

  methods: {
    setLocalStatus(){
      this.localStatus = this.status
    }
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
    status: String,
    studentId: String
  }
}
</script>

