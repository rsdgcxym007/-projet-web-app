<template>
  <v-container class="my-16" fluid>
    <v-row align="center" justify="center">
      <v-col cols="20" sm="20" md="10" lg="5">
        <v-row align="center"> </v-row>
        <v-form ref="form" v-model="valid" lazy-validation>
          <br />
          <h2 align="center">อัพเดทอาการปัจจุบัน</h2>
          <br />
          <v-textarea
            v-model="updatecurr"
            counter
            label="อัพเดทอาการปัจจุบัน"
            :rules="updatecurrRules"
            :value="value"
            required
          ></v-textarea>
          <v-btn color="error" class="mr-4" @click="black"> ย้อนกลับ</v-btn>
          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="validate"
          >
            บันทึกข้อมูล
          </v-btn>
          <v-btn color="error" class="mr-4" @click="reset"> Reset Form </v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  data: () => ({
    valid: true,
    updatecurr: '',
    updatecurrRules: [
      (v) => !!v || 'กรุณาใส่ที่อยู่',
      (v) => (v && v.length <= 100) || 'กรุณาใส่ที่อยู่',
    ],
  }),
  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    black() {
      this.$refs.form.black()
    },
  },
}
</script>
