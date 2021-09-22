<!-- Please remove this file from your project -->
<template>
  <div>
    list of the students, given we have selected {{ selectado }}
  </div>
</template>

<script>
export default {
  computed: {
    selectado(){
      return this.$store.state.selectado
    }
  }
}
</script>
