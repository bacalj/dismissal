<!-- Please remove this file from your project -->
<template>
  <div>
    <Student
      v-for="s in allStudents" :key="s.id" :s="s"
      v-show="amInFilter(s)"
    />
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

  /*
    filter nearly working, I think I have to watch selectado, and when it changes, call amInFilter or run filters in some other way, look and see what you did on self-evident
  */
  computed: {
    selectado(){
      return this.$store.state.selectado
    }
  },

  methods: {
    amInFilter(x){
      if ( this.$store.state.selectado == null){
        return true
      }

      else {
        if (x.class == this.$store.state.selectado){
          return true
        }

        else {
          return false
        }
      }
    },

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
