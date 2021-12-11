<template>
  <div>
    profile
    <pre>{{ $auth.user }}</pre>

    <v-btn color="red" @click="logout">logout</v-btn>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  methods: {
    async logout() {
      await this.$auth.logout()
      this.$router.push('/user/auth')
    },
  },
}
</script>
