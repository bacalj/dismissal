<template>
  <div v-show="amInFilter" class="rounded shadow overflow-hidden pl-3 bg-white mb-2">
    <div class="p-1">
      <div class="py-3 name">{{ first }} {{ last }}</div>
      <div class="py-3 room">{{ room }}</div>
    </div>
    <div class="p-1 flex justify-between">

        <button
          :id="`${studentId}_walking`"
          class="flex cursor-pointer py-3 px-5 w-1/3"
          :class="{ activo : status == 'walking'}"
          @click="setStudentStatus('walking')"
        >
          🚸 Walking
        </button>

        <button
          :id="`${studentId}_waiting`"
          class="flex cursor-pointer py-3 px-5 w-1/3"
          :class="{ activo : status == 'waiting'}"
          @click="setStudentStatus('waiting')"
        >
          ⏳ Waiting
        </button>

        <button
          :id="`${studentId}_rides-here`"
          class="flex cursor-pointer py-3 px-5 w-1/3"
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

  methods: {
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
