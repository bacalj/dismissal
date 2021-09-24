<template>
  <div>
    {{ s.first }} {{ s.last }} | {{ s.class }} <em>{{ s.status }}</em>
  </div>
</template>

<script>
export default {
  props: {
    s: Object
  }
}
</script>
