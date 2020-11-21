<template>
    <v-container>
        <v-row>
            <v-col>
                <v-card>
                    <v-card-title class="headline font-weight-black">
                    Add Product
                    </v-card-title>
                    <v-container>
                        <v-row>
                            <v-col class="font-weight">
                                Product Details
                                <template>
                                    <v-form
                                        ref="form"
                                        v-model="valid"
                                        lazy-validation
                                    >
                                        <v-text-field
                                        v-model="name"
                                        :rules="nameRules"
                                        label="Name"
                                        required
                                        ></v-text-field>

                                        <v-select
                                        v-model="select"
                                        :items="items"
                                        :rules="[v => !!v || 'Category is required']"
                                        label="Category"
                                        required
                                        ></v-select>

                                        <v-text-field
                                        v-model="hpp" 
                                        :rules="hppRules"
                                        label="HPP"
                                        required
                                        ></v-text-field>

                                        <v-text-field
                                        v-model="price" 
                                        :rules="priceRules"
                                        label="Price"
                                        required
                                        ></v-text-field>

                                        <v-btn
                                        :disabled="!valid"
                                        color="success"
                                        class="mr-4"
                                        @click="validate"
                                        >
                                        Validate
                                        </v-btn>

                                        <v-btn
                                        color="error"
                                        class="mr-4"
                                        @click="reset"
                                        >
                                        Reset Form
                                        </v-btn>
                                    </v-form>
                                </template>
                            </v-col>
                            <v-col class="font-weight">
                                Ingredients
                            </v-col>
                        </v-row>
                    </v-container>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
  export default {
    head() {
        return {
        title: 'Produk',
        }
    },
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
      ],
      hpp: '',
      hppRules: [
        v => !!v || 'HPP is required',
      ],
      price: '',
      priceRules: [
        v => !!v || 'Price is required',
      ],
      select: null,
      items: [
        'Food',
        'Beverage',
        'Dessert',
      ],
      checkbox: false,
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