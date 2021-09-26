<template>
<div>room: {{ classroom }} </div>
</template>

<script>
export default {
  computed: {
    classroom(){
      return this.$route.params.slug
    }
  }
}
</script>
