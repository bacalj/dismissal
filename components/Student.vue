<template>
  <div v-show="amInFilter" class="rounded border border-gray-600 overflow-hidden bg-gray-100 mb-2">
    <div class="flex justify-between">
      <div class="pl-3 py-3 name">{{ first }} {{ last }}</div>
      <div class="py-3 room pr-3">{{ room }}</div>
    </div>
    <div class="flex justify-between text-center">

        <button
          :id="`${studentId}_walking`"
          class="text-center border-r border-t border-gray-300 bg-white cursor-pointer py-3 px-5 w-1/3"
          :class="{ activo : status == 'walking'}"
          @click="setStudentStatus('walking')"
        >
          🚸 Walking
        </button>

        <button
          :id="`${studentId}_waiting`"
          class="text-center border-r border-t border-gray-300 bg-white cursor-pointer py-3 px-5 w-1/3"
          :class="{ activo : status == 'waiting'}"
          @click="setStudentStatus('waiting')"
        >
          ⏳ Waiting
        </button>

        <button
          :id="`${studentId}_rides-here`"
          class="text-center bg-white border-t border-gray-300 cursor-pointer py-3 px-5 w-1/3"
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

button {
  text-align: center;
}
.activo {
  @apply bg-blue-200
}

</style>
