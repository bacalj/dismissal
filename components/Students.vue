<!-- Please remove this file from your project -->
<template>
  <div>
    <Student v-for="s in showThese" :key="s.id" :s="s" />
  </div>
</template>

<script>
export default {
  data(){
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
      console.log('computing showThese')
      console.log(this.selectado)

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

        snap.docChanges().forEach((change) => {

          if (change.type === "modified") {

            // 1 find address of the changed student in allStudents
            const thisOne = this.allStudents.findIndex((student) => {
              return student.id == change.doc.id
            })

            // 2 set that students status to the new status
            this.$set(this.allStudents[thisOne], 'status', change.doc.data().status)
          }


        })
      })
    }
  }
}
</script>
