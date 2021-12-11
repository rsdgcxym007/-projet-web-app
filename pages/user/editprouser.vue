<template>
  <v-row justify="center my-16">
    <v-col cols="12" sm="10" md="8" lg="6">
      <v-card ref="form">
        <v-card-text>
          <v-text-field
            ref="name"
            v-model="name"
            :rules="[() => !!name || 'This field is required']"
            :error-messages="errorMessages"
            label=" Name"
            placeholder="John Doe"
            required
          ></v-text-field>
          <v-text-field
            ref="Lastname"
            v-model="Lastname"
            :rules="[() => !!Lastname || 'This field is required']"
            :error-messages="errorMessages"
            label=" LastName"
            placeholder="dddJohn Doe"
            required
          ></v-text-field>
          <v-text-field
            ref="address"
            v-model="address"
            :rules="[
              () => !!address || 'This field is required',
              () =>
                (!!address && address.length <= 100) ||
                'Address must be less than 100 characters',
              addressCheck,
            ]"
            label="Address"
            placeholder="Snowy Rock Pl"
            counter="100"
            required
          ></v-text-field>
          <v-text-field
            ref="tel"
            v-model="tel"
            :rules="[() => !!state || 'This field is required']"
            label="Tel"
            required
            placeholder="TX"
          ></v-text-field>
        </v-card-text>
        <v-divider class="mt-12"></v-divider>
        <v-card-actions>
          <v-btn text> Cancel </v-btn>
          <v-spacer></v-spacer>
          <v-slide-x-reverse-transition>
            <v-tooltip v-if="formHasErrors" left>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  icon
                  class="my-0"
                  v-bind="attrs"
                  @click="resetForm"
                  v-on="on"
                >
                  <v-icon>mdi-refresh</v-icon>
                </v-btn>
              </template>
              <span>Refresh form</span>
            </v-tooltip>
          </v-slide-x-reverse-transition>
          <v-btn color="primary" text @click="submit"> Submit </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data: () => ({
    errorMessages: '',
    name: null,
    Lastname: null,
    address: null,
    tel: null,
    formHasErrors: false,
  }),

  computed: {
    form() {
      return {
        name: this.name,
        Lastname: this.Lastname,
        address: this.address,
        tel: this.tel,
      }
    },
  },

  watch: {
    name() {
      this.errorMessages = ''
    },
  },

  methods: {
    addressCheck() {
      this.errorMessages = this.address && !this.name ? `Hey! I'm required` : ''

      return true
    },
    resetForm() {
      this.errorMessages = []
      this.formHasErrors = false

      Object.keys(this.form).forEach((f) => {
        this.$refs[f].reset()
      })
    },
    submit() {
      this.formHasErrors = false

      Object.keys(this.form).forEach((f) => {
        if (!this.form[f]) this.formHasErrors = true

        this.$refs[f].validate(true)
      })
    },
  },
}
</script>
