<template>
  <div>
    <!-- <pre>{{ types }}</pre> -->
    <v-container>
      <v-row>
        <v-col cols="12" sm="6" md="12">
          <v-autocomplete
            v-model="body.type"
            :items="types"
            dense
            filled
            label="ประเภท"
          ></v-autocomplete>
        </v-col>
        <v-col cols="12">
          <v-textarea
            v-model="body.remark"
            label="คำอธิบายอาการเบื้องต้น"
          ></v-textarea>
        </v-col>
        <v-col cols="12">
          <v-btn color="success" @click="request()">Request</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios }) {
    const { result: types } = await $axios.$get('/api/master/type')

    return { types }
  },
  data() {
    return {
      body: {
        type: '',
        remark: '',
        user_id: this.$auth.user.id,
        status_id: 1,
      },
    }
  },
  methods: {
    async request() {
      const { result, message } = await this.$axios.$post(
        '/api/manage/request',
        this.body
      )

      if (!result) {
        console.log('error : ', message)
      } else {
        this.$swal({
          type: 'success',
          title: message,
        })
        this.$router.push({ path: '/manage' })
      }
    },
  },
}
</script>
