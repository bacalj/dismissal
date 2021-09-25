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

  created(){
    this.setInitialData()
  },

  mounted(){
    this.handleIncomingChanges()
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



 /* ok lets do patches in moounted but initial load in asyncData or created() */
  methods: {
    async setInitialData(){
      this.$fire.firestore.collection("students").get().then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          let studentObj = { id: doc.id, first: doc.data().first, last: doc.data().last, status: doc.data().status }
          this.allStudents.push(studentObj)
        });
      });
    },

    async handleIncomingChanges() {
      const studentsRef = this.$fire.firestore.collection('students')

      studentsRef.onSnapshot((snap) =>{
        let changes = snap.docChanges()
        changes.forEach((change) => {

          if (change.type === "modified") {

            let idToChange = change.doc.id
            let newStatus = change.doc.data().status

            // 1 find address of the changed student in allStudents
            const indexOfStudent = this.allStudents.findIndex((student) => {
              return student.id == idToChange
            })

            // 2 set that students status to the new status
            this.$set(this.allStudents[indexOfStudent], 'status', newStatus)
          }


        })
      })
    }
  }
}
</script>
