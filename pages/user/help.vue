<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="6" lg="6">
        <v-text-field
          v-model="name"
          :rules="nameRules"
          label="ชื่อผู้ติดต่อ"
          required
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="6" lg="6">
        <v-text-field
          v-model="line"
          :rules="lineRules"
          label="ช่องทางติดต่ออืนๆ"
          required
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="6" lg="6">
        <v-text-field
          v-model="line"
          :rules="lineRules"
          label="ช่องทางติดต่ออืนๆ"
          required
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="6" lg="6">
        <v-text-field
          v-model="phone"
          :counter="10"
          :rules="phoneRules"
          label="เบอร์โทร"
          required
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="12" lg="12">
        <v-textarea
          v-model="symptom"
          counter
          label="อาการเบื้องต้น"
          :rules="symptomRules"
          :value="value"
          required
        ></v-textarea>
      </v-col>
      <v-col cols="12" md="12" lg="12">
        <v-textarea
          v-model="add"
          counter
          label="ที่อยู่ปัจจุบัน"
          :rules="addRules"
          :value="value"
          required
        ></v-textarea>
      </v-col>
      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        บันทึกข้อมูล
      </v-btn>
      <v-btn color="error" class="mr-4" @click="reset"> Reset Form </v-btn>
    </v-row>
  </v-container>
</template>
<script>
export default {
  data: () => ({
    valid: true,
    add: '',
    addRules: [
      (v) => !!v || 'กรุณาใส่ที่อยู่',
      (v) => (v && v.length <= 100) || 'กรุณาใส่ที่อยู่',
    ],
    name: '',
    nameRules: [
      (v) => !!v || 'กรุณากรอกชื่อ',
      (v) => (v && v.length <= 30) || 'กรุณากรอกชื่อ',
    ],
    line: '',
    lineRules: [
      (v) => !!v || 'กรุณาใส่ข้อมูล',
      (v) => (v && v.length <= 30) || 'กรุณาใส่ข้อมูล',
    ],
    phone: '',
    phoneRules: [
      (v) => !!v || 'กรุณาใส่เบอร์โทร',
      (v) => (v && v.length <= 10) || 'กรุณาใส่เบอร์โทร',
    ],
    symptom: '',
    symptomRules: [
      (v) => !!v || 'กรุณาใส่อาการเบื้องต้น',
      (v) => (v && v.length <= 10) || 'กรุณาใส่อาการเบื้องต้น',
    ],
  }),

  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
  },
}
</script>
