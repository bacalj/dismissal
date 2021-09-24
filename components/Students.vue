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
      allStudents: []
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

      studentsRef.onSnapshot((snap) =>{
        let changes = snap.docChanges()
        changes.forEach((change) => {
          console.log(change.doc.data())
        })
      })
      // studentsRef.onSnapshot((snapshot) => {
      //     snapshot.docChanges.forEach((change) => {
      //       console.log(change.doc.data())
      //     })
      //   })
      // })

      /* ok client is notified of change, just have to make store react, try it , but if not work, maybe a manual patch using the change object you get back from firestore like in this so-so SO example: https://stackoverflow.com/questions/62464830/updating-a-list-on-vuejs-by-using-the-real-time-change-listener-on-firestore */

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
