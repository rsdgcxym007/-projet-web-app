<template>
  <div>
    <v-container>
      <v-btn color="info" class="mb-6" @click="request">ขอความช่วยเหลือ</v-btn>
      <v-btn color="error" class="mb-6" @click="logout">ออกจากระบบ</v-btn>
      <v-card>
        <v-card-title>
          รายการคำร้องขอ
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
          ></v-text-field>
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="details"
          :items-per-page="50"
          :search="search"
          class="elevation-1"
        >
          <template v-slot:[`item.status_name`]="{ item }">
            <v-chip :color="item.color">
              {{ item.status_name }}
            </v-chip>
          </template>
        </v-data-table>
      </v-card>
    </v-container>
  </div>
</template>

<script>
export default {
  props: ['headers', 'details'],
  data() {
    return {
      search: '',
    }
  },
  methods: {
    request() {
      this.$router.push({ path: '/manage/request' })
    },
    async logout() {
      await this.$auth.logout()
      this.$router.push('/')
    },
  },
}
</script>
