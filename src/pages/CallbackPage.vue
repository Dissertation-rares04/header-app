<template>
  <q-page class="flex flex-center">
    {{ error }}
  </q-page>
</template>

<script>
export default {
  name: 'CallbackPage',
  data () {
    return {
      error: this.$auth0.error
    }
  }
}
</script>
