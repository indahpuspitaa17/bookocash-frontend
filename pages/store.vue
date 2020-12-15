<template>
  <v-card>
    <v-card-title>
      <span class="font-weight-bold"> Store Profile </span>
    </v-card-title>
    <v-row>
      <!-- STORE PROFILE -->
      <v-col class="px-6 ma-2">
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-text-field
            v-model="input.name"
            :counter="12"
            :rules="nameRules"
            label="Restaurant Name"
            required
          ></v-text-field>

          <v-text-field
            v-model="input.address"
            :counter="100"
            :rules="addressRules"
            label="Address"
            required
          ></v-text-field>

          <v-text-field
            v-model="input.owner"
            :counter="30"
            :rules="ownerRules"
            label="Owner Name"
            required
          ></v-text-field>

          <v-text-field
            v-model="input.phone"
            :counter="12"
            :rules="phoneRules"
            label="Phone"
          ></v-text-field>

          <v-text-field
            v-model="input.email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>

          <v-file-input
            label="Click to upload profile picture"
            filled
            prepend-icon="mdi-camera"
            v-model="input.photo"
          ></v-file-input>

          <v-btn color="error" class="mr-4" @click="reset"> Reset Form </v-btn>

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
        <v-container class="pa-0 ma-0 d-flex justify-center">
          <v-img
            max-height="150"
            max-width="250"
            :src="!!preview ? preview : '/images/default.png'"
          ></v-img>
        </v-container>
        <v-container class="pa-0 ma-0">
          <v-row class="pa-1 ma-0">
            <v-col cols="12" class="pa-0">
              <span
                class="font-weight-medium caption red--text text--lighten-2"
              >
                Restaurant name
              </span>
            </v-col>
            <v-col cols="12" class="pa-0">
              <span class="body-1"> {{ store.name }} </span>
            </v-col>
          </v-row>
          <v-row class="pa-1 ma-0">
            <v-col cols="12" class="pa-0">
              <span
                class="font-weight-medium caption red--text text--lighten-2"
              >
                Address
              </span>
            </v-col>
            <v-col cols="12" class="pa-0">
              <span class="body-1"> {{ store.address }} </span>
            </v-col>
          </v-row>
          <v-row class="pa-1 ma-0">
            <v-col cols="12" class="pa-0">
              <span
                class="font-weight-medium caption red--text text--lighten-2"
              >
                Owner name
              </span>
            </v-col>
            <v-col cols="12" class="pa-0">
              <span class="body-1"> {{ store.owner }} </span>
            </v-col>
          </v-row>
          <v-row class="pa-1 ma-0">
            <v-col cols="12" class="pa-0">
              <span
                class="font-weight-medium caption red--text text--lighten-2"
              >
                Email
              </span>
            </v-col>
            <v-col cols="12" class="pa-0">
              <span class="body-1"> {{ store.email }} </span>
            </v-col>
          </v-row>
          <v-row class="pa-1 ma-0">
            <v-col cols="12" class="pa-0">
              <span
                class="font-weight-medium caption red--text text--lighten-2"
              >
                Phone
              </span>
            </v-col>
            <v-col cols="12" class="pa-0">
              <span class="body-1"> {{ store.phone }} </span>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  head() {
    return {
      title: "Store",
    };
  },
  data: () => ({
    valid: true,
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => (v && v.length <= 12) || "Name must be less than 12 characters",
    ],
    addressRules: [
      (v) => !!v || "Address is required",
      (v) =>
        (v && v.length <= 100) || "Address must be less than 100 character",
    ],
    ownerRules: [
      (v) => !!v || "Owner name is required",
      (v) => (v && v.length <= 30) || "Address must be less than 30 character",
    ],
    phoneRules: [
      (v) => !!v || "Phone number is required",
      (v) =>
        (v && v.length <= 12) || "Phone number must be less than 12 character",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    select: null,
    store: {
      name: "Bungsu Sari",
      address: "Jl. Babakan Raya, Bogor, Jawa Barat",
      owner: "Sutardji Sudjono",
      email: "bungsusari@gmail.com",
      phone: "081234567810",
      photo: null,
    },
    input: {
      name: "Bungsu Sari",
      address: "Jl. Babakan Raya, Bogor, Jawa Barat",
      owner: "Sutardji Sudjono",
      email: "bungsusari@gmail.com",
      phone: "081234567810",
      photo: null,
    },
    preview: "",
  }),
  watch: {
    "store.photo"(v) {
      if (v) this.setPreview(v);
    },
  },
  methods: {
    validate() {
      if (!this.$refs.form.validate()) return;
      this.store.name = this.input.name;
      this.store.address = this.input.address;
      this.store.email = this.input.email;
      this.store.owner = this.input.owner;
      this.store.phone = this.input.phone;
      this.store.photo = this.input.photo;
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    setPreview(file) {
      const reader = new FileReader();
      reader.onload = (e) => {
        this.preview = e.target.result;
      };
      reader.readAsDataURL(file);
    },
  },
};
</script>