<template>
<div>room: {{ classRoom }} </div>
</template>

<script>
export default {
  computed: {
    classRoom(){
      return this.$route.params.slug
    }
  }
}
</script>
