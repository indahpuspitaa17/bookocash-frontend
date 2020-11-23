<template>
  <v-card>
    <v-card-title>
      <span class="font-weight-bold"> Store Profile </span>
    </v-card-title>
    <v-row>
      <!-- STORE PROFILE -->
      <v-col class="px-6 ma-2">
        <v-form
            ref="form"
            v-model="valid"
            lazy-validation
        >
          <v-text-field
          v-model="name"
          :counter="10"
          :rules="nameRules"
          label="Restaurant Name"
          required
          ></v-text-field>

          <v-text-field
              v-model="address"
              :counter="100"
              :rules="addressRules"
              label="Address"
              required
          ></v-text-field>

          <v-text-field
              v-model="owner"
              :counter="30"
              :rules="ownerRules"
              label="Owner Name"
              required
          ></v-text-field>

          <v-text-field
              v-model="phone"
              :counter="12"
              :rules="phoneRules"
              label="Phone"
          ></v-text-field>

          <v-text-field
          v-model="email"
          :rules="emailRules"
          label="E-mail"
          required
          ></v-text-field>

          <v-file-input
            label="Click to upload profile picture"
            filled
            prepend-icon="mdi-camera"
          ></v-file-input>

          <v-btn
          color="error"
          class="mr-4"
          @click="reset"
          >
          Reset Form
          </v-btn>

          <v-btn
          :disabled="!valid"
          color="success"
          class="mr-4"
          @click="validate"
          >
          Update
          </v-btn>
        </v-form>
      </v-col>

      <!-- UPDATED STORE PROFILE -->
      <v-col class="px-6 ma-2">
      haindah
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
  export default {
    head() {
    return {
      title: 'Store',
      script: [
        {src:'/store.js'}
      ]
    }
  },
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters',
      ],
      addressRules: [
          v => !!v || 'Address is required',
          v => (v && v.length <= 100) || 'Address must be less than 100 character',
      ],
      ownerRules: [
          v => !!v || 'Owner name is required',
          v => (v && v.length <= 30) || 'Address must be less than 30 character',
      ],
      phoneRules: [
          v => !!v || 'Phone number is required',
          v => (v && v.length <= 12) || 'Phone number must be less than 12 character'
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      select: null,
    }),

    methods: {
      validate () {
        this.$refs.form.validate()
      },
      reset () {
        this.$refs.form.reset()
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
    },
  }
</script>