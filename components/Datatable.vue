<template>
  <div>
    <v-container>
      <!-- <v-btn color="info" class="mb-6" @click="request">ขอความช่วยเหลือ</v-btn>
      <v-btn color="info" class="mb-6" @click="update">อัพเดทอาการปัจจุบัน</v-btn>
      <v-btn color="info" class="mb-6" @click="upcovid">ทำเรื่องหายป่วย</v-btn>
      <v-btn color="error" class="mb-6" @click="logout">ออกจากระบบ</v-btn> -->
      <v-card>
        <v-card-title>
          รายการคำร้องขอ
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="ค้นหา"
          ></v-text-field>
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="details"
          :items-per-page="5"
          :search="search"
          class="elevation-1"
        >
          <template v-slot:[`item.status_name`]="{ item }">
            <v-chip :color="item.color">
              {{ item.status_name }}
            </v-chip>
          </template>
          <!-- <template v-slot:[`item.help`]="{}">
            <v-btn>ช่วยเหลือ</v-btn>
          </template> -->
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
    // request() {
    //   this.$router.push({ path: '/manage/request' })
    // },
    // upcovid() {
    //   this.$router.push({ path: '/manage/upcovid' })
    // },
    // update() {
    //   this.$router.push({ path : '/manage/update'})
    // },
    // async logout() {
    //   await this.$auth.logout()
    //   this.$router.push('/')
    // },
  },
}
</script>
