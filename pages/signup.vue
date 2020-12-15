<template>
  <v-container style="height: 100%">
    <v-row
      justify="center"
      align="center"
      align-content="center"
      style="height: 100%"
    >
      <v-col cols="12" sm="10" md="5" lg="5" align-self="center">
        <v-card class="pa-5" flat>
          <v-card-title
            class="headline font-weight-bold text-uppercase text-center"
          >
            <v-spacer></v-spacer>
            <span>Sign Up</span>
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
                    :label="'Username'"
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
                    :label="'Password'"
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
              type="submit"
              @click.stop="signup()"
              >Sign Up</v-btn
            >
          </v-card-actions>

          <v-card-actions>
            <v-btn outlined block color="#363062" @click.stop="$router.go(-1)"
              >Kembali</v-btn
            >
          </v-card-actions>
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
  layout: "blank",
  head() {
    return {
      title: "Sign Up",
    };
  },
  data() {
    return {
      alert: false,
      success: false,
      messages: "",
      show: false,
      input: {
        email: null,
        password: null,
      },
      rules: {
        required: (value) =>
          !!value || `${this.$("text.required", "capitalize")}`,
        min: (value) => (!!value && value.length >= 6) || "Minimum 6",
        email: (value) =>
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
            value
          ) || `${this.$("helper.wrong_email", "capitalize")}`,
      },
      methods: {
        async register() {
          if (!this.$refs.form.validate()) {
            this.success = false;
            this.messages = "Periksa kembali data yang diinput";
            this.alert = true;
            return;
          }
          try {
            const result = await this.$api("user", "register", this.input);
            if (result.status === 201) {
              this.success = true;
              this.messages = "User berhasil dibuat";
              this.alert = true;
            }
          } catch (e) {
            this.success = false;
            this.messages = "Gagal register user";
            this.alert = true;
          }
        },
      },
    };
  },
};
</script>
<style scoped></style>
