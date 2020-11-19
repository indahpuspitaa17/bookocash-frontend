<template>
  <v-container style="height: 100%">
    <v-row
      justify="center"
      align="center"
      align-content="center"
      style="height: 100%"
    >
      <v-col cols="12" sm="1" md="2" lg="5" align-self="center">
        <v-card class="pa-5" >
          <v-card-title
            class="headline font-weight-bold text-uppercase text-center"
          >
            <v-spacer></v-spacer>
            <span>Login</span>
            <v-divider class="mx-2" vertical></v-divider>
            <span class="4d4c7d--text">bookocash.id</span>
            <v-spacer></v-spacer>
          </v-card-title>
          <v-card-subtitle class="caption text-center"
            >Masukan akun yang telah terdaftar</v-card-subtitle
          >
          
          <v-card-text>
            <v-form ref="form">
              <v-row>
                <v-col cols="12">
                  <v-text-field
                    v-model="input.email"
                    prepend-inner-icon="mdi-account"
                    color="#363062"
                    solo
                    :label="('Username')"
                    counter
                    autofocus
                    @keyup.enter="login()"
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    v-model="input.password"
                    prepend-inner-icon="mdi-lock"
                    color="#363062"
                    solo
                    :label="('Password')"
                    :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                    :type="show ? 'text' : 'password'"
                    counter
                    @click:append="show = !show"
                    @keyup.enter="login()"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-form>
          </v-card-text>

          <v-card-actions>
            <v-btn
              large
              color="#363062"
              block
              dark
              elevation="8"
              @click.stop="login()"
              >Login</v-btn
            >
          </v-card-actions>
          <v-card-text class="text-center">
            <span class="caption">
              Don't have account?
            </span>
            <nuxt-link 
                to="/signup"
                class="caption" 
                color="#363062"
            ><b>Let's sign up!</b></nuxt-link>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <snackbar-alert
      v-model="alert"
      :success="success"
      :messages="messages"
    ></snackbar-alert>
  </v-container>
</template>
<script>
export default {
  layout: 'blank',
  data() {
    return {
      alert: false,
      success: false,
      messages: '',
      show: false,
      input: {
        email: null,
        password: null
      },
      rules: {
        required: (value) =>
          !!value || `${this.$('text.required', 'capitalize')}`,
        min: (value) => (!!value && value.length >= 6) || 'Minimum 6',
        email: (value) =>
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
            value
          ) || `${this.$('helper.wrong_email', 'capitalize')}`
      }
    }
  },
  mounted() {},
  methods: {
    async login() {
      if (!this.$refs.form.validate()) {
        this.success = false
        this.messages = `${this.$translate(
          'alert.login.warning',
          'capitalize'
        )}`
        this.alert = true
        return
      }
      try {
        const result = await this.$api('user', 'login', this.input)
        if (result.status === 200) {
          this.success = true
          this.messages = `${this.$translate(
            'alert.login.success',
            'capitalize'
          )}`
          this.alert = true
        } else {
          this.success = false
          this.messages = `${this.$translate(
            'alert.login.error',
            'capitalize'
          )}`
          this.alert = true
        }
      } catch (e) {
        this.success = false
        this.messages = `${this.$translate('alert.error')}` + e.toString()
        this.alert = true
      }
    }
  }
}
</script>
<style scoped></style>
