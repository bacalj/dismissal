<template>
  <div v-show="amInFilter" class="rounded shadow pl-3 bg-white mb-2 flex justify-betweeen">
    <div class="py-3 name w-1/3">{{ first }} {{ last }}</div>
    <div class="py-3 room w-1/6">{{ room }}</div>

    <div class="status-radio w-1/2 text-right">

        <button
          :id="`${studentId}_walking`"
          class="-mr-1 cursor-pointer py-3 px-5"
          :class="{ activo : status == 'walking'}"
          @click="setStudentStatus('walking')"
        >
          🚸 Walking
        </button>

        <button
          :id="`${studentId}_waiting`"
          class="-mr-1 cursor-pointer py-3 px-5"
          :class="{ activo : status == 'waiting'}"
          @click="setStudentStatus('waiting')"
        >
          ⏳ Waiting
        </button>

        <button
          :id="`${studentId}_rides-here`"
          class="-mr-1 cursor-pointer py-3 px-5"
          :class="{ activo : status == 'rides-here'}"
          @click="setStudentStatus('rides-here')"
        >
          🚗 Ride Here
        </button>

    </div>
  </div>
</template>

<script>


export default {

  watch: {
    localStatus(val, oldVal) {
      this.setStudentStatus(val)
    },

    status(n,o){
      this.setLocalStatus()
    }
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
    },

    async setStudentStatus(value){
      const studentRef = this.$fire.firestore.collection('students').doc(this.studentId)
      try {
        await studentRef.update({status: value})
      } catch(e) {
        alert(e)
        return
      }
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

<style lang="postcss" scoped>

.activo {
  @apply bg-blue-200 shadow
}

</style>
