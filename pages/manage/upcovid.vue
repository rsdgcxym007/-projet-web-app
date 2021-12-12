<template>
  <v-container class="my-16" fluid>
    <v-row align="center" justify="center">
      <v-col cols="12" sm="10" md="6" lg="4">
        <v-row align="center"> </v-row>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-text-field
            v-model="date"
            :rules="dateRules"
            label="เข้ารับการตรวจเมื่อวันที่"
            required
          ></v-text-field>

          <v-text-field
            v-model="hospi"
            :rules="hospiRules"
            label="ระบุชื่อโรงพยาบาล ที่เข้ารับการตรวจ"
            required
          ></v-text-field>
          <v-file-input
            accept="image/*"
            label="ผลตรวจเชื้อแบบ RT-PCR"
          ></v-file-input>
          <v-file-input accept="image/*" label="ใบรับรองแพทย์"></v-file-input>
        </v-form>
         <v-btn color="error" class="mr-4" @click="black"> ย้อนกลับ</v-btn>
        <v-btn
          :disabled="!valid"
          color="success"
          class="mr-4"
          @click="validate"
        >
          บันทึกข้อมูล
        </v-btn>
        
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  data: () => ({
    middleware: 'auth',
    valid: true,
    date: '',
    dateRules: [
      (v) => !!v || 'กรุณากรอกชื่อ',
      (v) => (v && v.length <= 30) || 'กรุณากรอกชื่อ',
    ],
    hos: '',
    hosRules: [
      (v) => !!v || 'กรุณาใส่ข้อมูล',
      (v) => (v && v.length <= 30) || 'กรุณาใส่ข้อมูล',
    ],
  }),

  methods: {
    validate() {
      this.$refs.form.validate()
    },
    black() {
      this.$router.push({ path: '/manage' })
    },
  },
}
</script>
