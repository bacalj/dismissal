<template>
  <div class="p-12">
    <div>room: {{ classroom }} </div>
    <ul>
      <li v-for="s in studentsInRoom" :key="s.id">
        {{ s.first }} {{ s.last }}: {{ s.status }}
      </li>
    </ul>
  </div>

</template>

<script>
export default {
  data(){
    return {
      studentsInRoom: []
    }
  },

  created(){
    this.setInitialData()
  },

  mounted(){
    this.handleIncomingChanges()
  },

  computed: {
    classroom(){
      return this.$route.params.slug
    }
  },

  methods: {
    async setInitialData(){
      this.$fire.firestore.collection("students").where("room", "==", this.classroom)
        .get().then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          let studentObj = {
            id: doc.id,
            first: doc.data().first,
            last: doc.data().last,
            status: doc.data().status,
            room: doc.data().room
          }
          this.studentsInRoom.push(studentObj)
        });
      });
    },

    async handleIncomingChanges() {
      const studentsRef = this.$fire.firestore.collection('students')

      studentsRef.onSnapshot((snap) =>{

        snap.docChanges().forEach((change) => {

          if (change.type === "modified") {

            // 1 find address of the changed student in studentsInRoom
            const thisOne = this.studentsInRoom.findIndex((student) => {
              return student.id == change.doc.id
            })

            // 2 set that students status to the new status
            this.$set(this.studentsInRoom[thisOne], 'status', change.doc.data().status)
          }


        })
      })
    }
  }
}
</script>

