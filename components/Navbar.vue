<template>
  <nav class="navbar">
    <div class="my-2">

        <h1 class="text-lg p-2">🚦 Campus School Dismissal Board</h1>

    </div>

    <div class="my-2 mx-2 pb-4 md:pb-0">
      <nuxt-link to="/">Dismiss View</nuxt-link>
      <nuxt-link to="/rooms">Classroom Views</nuxt-link>
    </div>
  </nav>
</template>

<style lang="postcss" scoped>
.navbar {
  @apply flex flex-col text-center sm:flex-row sm:text-left sm:justify-between bg-white shadow sm:items-baseline w-full;
}

a {
  @apply px-3 py-2 rounded border border-gray-200
}

a:hover {
  @apply bg-green-200 border-green-200
}
</style>
