<template>
  <div class="p-12 room green-text">
    <div>
      <h1 class="green-text">room: {{ classroom }}</h1>
    </div>
    <br><span class="green-text">---------</span>
    <ul>
      <li v-for="s in studentsInRoom" :key="s.id" class="green-text flex mb-2">
        <div class="w-1/4">
          {{ s.first }} {{ s.last }}
        </div>
        <div class="w-1/4">{{ s.status }}</div>
        <div class="w-1/4">
          <button class="ok">OK</button>
        </div>

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

<style lang="postcss" scoped>
.green-text {
  font-family: 'DotGothic16', monospace;
  color:rgb(153, 229, 153);
  @apply text-2xl;
}

.green-text.faded {
  color:rgb(87, 107, 87);
}

button.ok {
  color: rgb(31, 41, 55);
  background-color: rgb(153, 229, 153);
  @apply px-3
}
</style>
