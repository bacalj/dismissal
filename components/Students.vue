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

    async readFromFirestore() {
      const studentsRef = this.$fire.firestore.collection('students')

      studentsRef.onSnapshot((snap) =>{
        let changes = snap.docChanges()
        changes.forEach((change) => {

          if (change.type === "modified") {

            let idToChange = change.doc.id
            let newStatus = change.doc.data().status

            console.log(idToChange, " - should now be: ", newStatus)

            // 1 find item in array where change.doc.id == item.id
            const indexOfStudent = this.allStudents.findIndex((student) => {
              return student.id == idToChange
            })

            console.log(indexOfStudent)

            // 2 this.$set item.status to change.doc.data().status
           // this.$set(this.allStudents[indexOfStudent], 'status', change.doc.data().status)
          }


        })
      })
      // studentsRef.onSnapshot((snapshot) => {
      //     snapshot.docChanges.forEach((change) => {
      //       console.log(change.doc.data())
      //     })
      //   })
      // })

      /* ok client is notified of change, just have to make store react, try it , but if not work, maybe a manual patch using the change object you get back from firestore like in this so-so SO example: https://stackoverflow.com/questions/62464830/updating-a-list-on-vuejs-by-using-the-real-time-change-listener-on-firestore */


    }
  }
}
</script>
