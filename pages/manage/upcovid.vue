<template>
  <v-container class="my-16" fluid>
    <v-row align="center" justify="center">
      <v-col cols="12" sm="10" md="6" lg="4">
        <v-row align="center"> </v-row>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-file-input
            type="file"
            accept="image/*"
            label="ผลตรวจเชื้อแบบ RT-PCR"
            v-model="image1"
          ></v-file-input>
          <v-file-input
            accept="image/*"
            v-model="image2"
            label="ใบรับรองแพทย์"
          ></v-file-input>
        </v-form>
        <v-btn color="error" class="mr-4" @click="black"> ย้อนกลับ</v-btn>
        <v-btn :disabled="!valid" color="success" class="mr-4" @click="upload">
          บันทึกข้อมูล
        </v-btn>
        <!-- <v-img src="http://localhost:4000/image/file-1639411566287.jpg"></v-img> -->
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  middleware: 'auth',
  data: () => ({
    valid: true,
    date: null,
    hotpital_name: null,
    image1: null,
    image2: null,
  }),
  methods: {
    async upload() {
      // var fileBuffer = Buffer.from(this.image1)
      // console.log('fileBuffer : ', fileBuffer)

      console.log(this.hotpital_name)

      if (this.image1) {
        let formData = new FormData()
        formData.append('hotpital_name', this.hotpital_name)
        formData.append('date', this.date)
        formData.append('file', this.image1)

        await this.$axios
          .$post(`/api/upload`, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          })
          .then(async () => {
            if (this.image2) {
              let formData = new FormData()
              formData.append('file', this.image2)

              await this.$axios.$post(`/api/upload`, formData, {
                headers: {
                  'Content-Type': 'multipart/form-data',
                },
              })
            }
          })
      } else if (this.image2) {
        let formData = new FormData()
        formData.append('hotpital_name', this.hotpital_name)
        formData.append('date', this.date)
        formData.append('file', this.image2)

        await this.$axios
          .$post(`/api/upload`, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          })
          .then(async () => {
            if (this.image1) {
              let formData = new FormData()

              formData.append('file', this.image1)

              await this.$axios.$post(`/api/upload`, formData, {
                headers: {
                  'Content-Type': 'multipart/form-data',
                },
              })
            }
          })
      }
    },
    validate() {
      this.$refs.form.validate()
    },
    black() {
      this.$router.push({ path: '/manage' })
    },
  },
}
</script>
