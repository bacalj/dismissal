<!-- Please remove this file from your project -->
<template>
  <div>
    all students are in state from firebase, but filter based on <b>{{ selectado }}</b>
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

  computed: {
    selectado(){
      return this.$store.state.selectado
    },

    showThese(){
      // this will eventually be result of filter
      return this.allStudents
    }
  }
}
</script>
