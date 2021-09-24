<!-- Please remove this file from your project -->
<template>
  <div>
    <Student v-for="s in showThese" :key="s.id" :s="s" />
  </div>
</template>

<script>
export default {
  data(){
    // we'll get all the students from firebase and load them into state
    // should be reactive but if not we'll get it all in vuex or see what we did on reading app
    // still need to add in firebase credentials
    return {
      allStudents: [{'name' : 'Bobby', 'id' : 'abc'}, {'name' : 'Sally', 'id' : '123'}]
    }
  },

  mounted(){
    this.readFromFirestore()
  },

  computed: {
    selectado(){
      return this.$store.state.selectado
    },

    showThese(){
      // this will eventually be result of filter
      return this.allStudents
    }
  },

  methods: {
    async readFromFirestore() {
      const studentsRef = this.$fire.firestore.collection('students')
      const studentsCollection = await studentsRef.get().then((qs) => {
        qs.forEach((student) => {
          console.log(student.data())
        })
      })

      // try {
      //   const studentsCollection = await studentsRef.get()
      //   console.log(studdentsCollection)
      // }

      // catch (e) {
      //   alert(e)
      //   return
      // }
    }
  }
}
</script>
