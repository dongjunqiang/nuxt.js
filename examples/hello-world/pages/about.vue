<template>
  <div>
    <p>Hi from {{ name }}</p>
    <nuxt-link to="/">Home page</nuxt-link>
  </div>
</template>

<script>
export default {
  asyncData ({ isStatic, isServer }) {
    return {
      name: isStatic ? 'static' : (isServer ? 'server' : 'client')
    }
  }
}
</script>
