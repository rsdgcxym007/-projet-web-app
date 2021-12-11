<template>
  <div id="app">
    <v-app id="inspire">
      <v-app id="inspire">
        <v-main>
          <v-container class="fill-height" fluid>
            <v-row align="center" justify="center">
              <v-col cols="12" sm="10" md="6" lg="4">
                <v-card class="elevation-12">
                  <v-tabs v-model="tabs" fixed-tabs color="light-blue darken-4">
                    <v-tabs-slider></v-tabs-slider>
                    <v-tab href="#mobile-tabs-5-1">
                      <h3>เข้าสู่ระบบอาสาสมัคร</h3>
                    </v-tab>

                    <v-tab href="#mobile-tabs-5-2"> <h3>ลงทะเบียนอาสาสมัคร</h3> </v-tab>
                  </v-tabs>
                  <v-tabs-items v-model="tabs">
                    <v-tab-item :value="'mobile-tabs-5-1'">
                      <v-card flat>
                        <v-card-text>
                          <v-form ref="form1" v-model="valid1" lazy-validation>
                            <v-text-field
                              v-model="Email"
                              label="Email"
                              prepeFnd-icon="mdi-at"
                              type="text"
                              :rules="EmailRule"
                              autocomplete="off"
                              required
                              @keyup.enter="validate1"
                            ></v-text-field>

                            <v-text-field
                              id="password"
                              v-model="Password"
                              label="Password"
                              prepend-icon="mdi-lock"
                              autocomplete="off"
                              :rules="PasswordRule"
                              required
                              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                              :type="show1 ? 'text' : 'password'"
                              @click:append="show1 = !show1"
                              @keyup.enter="validate1"
                            ></v-text-field>
                          </v-form>
                        </v-card-text>
                        <v-card-actions>
                          <v-spacer></v-spacer>
                          <v-btn @click="reset1">Reset</v-btn>
                          <v-btn color="primary" @click="validate1"
                            ><v-icon>mdi-lock</v-icon>เข้าสู่ระบบ</v-btn
                          >
                        </v-card-actions>
                      </v-card>
                    </v-tab-item>
                    <v-tab-item :value="'mobile-tabs-5-2'">
                      <v-card flat>
                        <v-card-text>
                          <v-form ref="form2" v-model="valid2" lazy-validation>
                            <v-text-field
                              v-model="Name"
                              label="Name"
                              prepend-icon="mdi-account"
                              type="text"
                              required
                              :rules="NameRule"
                              autocomplete="off"
                              @keyup.enter="validate2"
                            ></v-text-field>
                            <v-text-field
                              v-model="Lastname"
                              label="Lastname"
                              prepend-icon="mdi-account"
                              type="text"
                              required
                              :rules="LastnameRule"
                              autocomplete="off"
                              @keyup.enter="validate2"
                            ></v-text-field>
                            <v-text-field
                              v-model="Position"
                              label="Position"
                              prepend-icon="mdi-clipboard-account"
                              autocomplete="off"
                              type="text"
                              required
                              :rules="PositionRule"
                              @keyup.enter="validate2"
                            ></v-text-field>

                            <v-text-field
                              v-model="Tel"
                              label="Tel"
                              prepend-icon="mdi-phone"
                              type="text"
                              required
                              autocomplete="off"
                              :rules="TelRule"
                              @keyup.enter="validate2"
                            ></v-text-field>
                            <v-text-field
                              v-model="RegisEmail"
                              label="Email"
                              :rules="RegisEmailRule"
                              autocomplete="off"
                              prepend-icon="mdi-at"
                              type="text"
                              required
                              @keyup.enter="validate2"
                            ></v-text-field>
                            <v-text-field
                              v-model="RegisPassword"
                              label="Password"
                              :rules="RegisPasswordRule"
                              prepend-icon="mdi-lock"
                              autocomplete="off"
                              required
                              :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
                              :type="show2 ? 'text' : 'password'"
                              @keyup.enter="validate2"
                              @click:append="show2 = !show2"
                            ></v-text-field>
                            <v-text-field
                              v-model="ConRegisPassword"
                              label="Confirm Password"
                              :rules="ConRegisPasswordRule"
                              prepend-icon="mdi-lock"
                              required
                              autocomplete="off"
                              :append-icon="show3 ? 'mdi-eye' : 'mdi-eye-off'"
                              :type="show3 ? 'text' : 'password'"
                              @keyup.enter="validate2"
                              @click:append="show3 = !show3"
                            ></v-text-field>
                          </v-form>
                        </v-card-text>
                        <v-card-actions>
                          <v-spacer></v-spacer>
                          <v-btn @click="reset2">Reset</v-btn>
                          <v-btn color="primary" @click="validate2"
                            >Register</v-btn
                          >
                        </v-card-actions>
                      </v-card>
                    </v-tab-item>
                  </v-tabs-items>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </v-main>
      </v-app>
    </v-app>
  </div>
</template>
<script>
export default {
   layout: 'emplty',
//   middleware: 'logged',
  data() {
    return {
      show1: false,
      show2: false,
      show3: false,
      tabs: null,
      valid1: true,
      valid2: true,
      Email: '',
      Password: '',
      EmailRule: [
        (v) => !!v || 'E-mail is required',
        (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      PasswordRule: [(v) => !!v || 'Password is required'],
      Name: '',
      Lastname: '',
      Position: '',
      Tel: '',
      RegisEmail: '',
      RegisPassword: '',
      ConRegisPassword: '',
      RegisEmailRule: [
        (v) => !!v || 'E-mail is required',
        (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      NameRule: [(v) => !!v || 'Name is required'],
      LastnameRule: [(v) => !!v || 'Lastname is required'],
      PositionRule: [(v) => !!v || 'Position is required'],
      TelRule: [(v) => !!v || 'Tel is required'],
      RegisPasswordRule: [
        (value) => !!value || 'Please type password.',
        (value) => (value && value.length >= 6) || 'minimum 6 characters',
      ],
      ConRegisPasswordRule: [
        (value) => !!value || 'type confirm password',
        (value) =>
          value === this.RegisPassword ||
          'The password confirmation does not match.',
      ],
    }
  },
  methods: {
    reset1() {
      this.$refs.form1.reset()
    },
    reset2() {
      this.$refs.form2.reset()
    },
    validate1() {
      if (this.$refs.form1.validate() === true) {
        this.onSubmit()
      } else {
        this.$swal({
          icon: 'warning',
          title: 'กรุณากรอกข้อมูลให้ครบถ้วน',
          timer: 3000,
        })
      }
    },
    validate2() {
      if (this.$refs.form2.validate() === true) {
        this.Register()
      } else {
        this.$swal({
          icon: 'warning',
          title: 'กรุณากรอกข้อมูลให้ครบถ้วน',
          timer: 3000,
        })
      }
    },
    // async onSubmit() {
    //   const body = { Email: this.Email, Password: this.Password }
    //   try {
    //     await this.$auth.loginWith('local', {
    //       data: body,
    //     })
    //     this.$router.push('/shop')
    //   } catch (e) {
    //     this.$swal({
    //       icon: 'error',
    //       title: 'Oops...',
    //       text: 'Email หรือ Password ไม่ถูกต้อง',
    //       timer: 3000,
    //     })
    //   }
    // },
    // async Register() {
    //   await this.$axios
    //     .post('/register', {
    //       Name: this.Name,
    //       Lastname: this.Lastname,
    //       Position: this.Position,
    //       Tel: this.Tel,
    //       Email: this.RegisEmail,
    //       Password: this.RegisPassword,
    //     })
    //     .then((res) => {
    //       this.$swal({
    //         icon: 'success',
    //         title: 'ลงทะเบียนสำเร็จ',
    //         showConfirmButton: false,
    //         timer: 3000,
    //       })
    //       this.reset2()
    //     })
    //     .catch((res) => {
    //       this.$swal({
    //         icon: 'error',
    //         title: 'Oops...',
    //         text: 'ลงทะเบียนไม่สำเร็จ',
    //         timer: 3000,
    //       })
    //     })
    // },
  },
}
</script>

<style></style>