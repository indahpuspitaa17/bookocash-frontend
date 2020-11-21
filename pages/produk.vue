<template>
    <v-container>
        <v-row>
            <v-col>
                <v-card>
                    <v-card-title>
                        <span class="headline">{{ formTitle }}</span>
                    </v-card-title>
                    <v-container>
                        <v-row>
                            <v-col class="pa-5 me-5">
                                <div class="font-weight-bold">
                                    Product Details
                                </div>
                                <template>
                                    <v-form
                                        ref="form"
                                        v-model="valid"
                                        lazy-validation
                                        class="me-8"
                                    >
                                        <v-text-field
                                        v-model="name"
                                        :rules="nameRules"
                                        label="Name"
                                        required
                                        ></v-text-field>

                                        <v-select
                                        v-model="select"
                                        :category="category"
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
                                    </v-form>
                                </template>
                            </v-col>
                            <v-col class="pa-5 me-5">
                                <v-col>
                                    <v-row class="font-weight-bold">
                                        Ingredients
                                    </v-row>
                                    <v-row class="mr-4 py-5">
                                        <v-btn
                                        color="#827397"
                                        >
                                        Add
                                        </v-btn>
                                    </v-row>
                                </v-col>
                            </v-col>
                        </v-row>
                        <v-card-actions>
                        <v-spacer></v-spacer>
                            <v-btn
                            color="error"
                            class="mr-4"
                            @click="close"
                            >
                            Cancel
                            </v-btn>

                            <v-btn
                            :disabled="!valid"
                            color="success"
                            class="mr-4"
                            @click="save"
                            >
                            Save
                            </v-btn>
                        </v-card-actions>
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

      category: [
        'Food',
        'Beverage',
        'Dessert',
      ],

      price: '',
      priceRules: [
        v => !!v || 'Price is required',
      ],

      hpp: '',
      hppRules: [
        v => !!v || 'HPP is required',
      ],
      
      editedIndex: -1,
      editedItem: {
        name: '',
        category: '',
        price: '',
        hpp: '',
      },
      defaultItem: {
        name: '',
        category: '',
        price: '',
        hpp: '',
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      },
    },

    methods: {
      getColor (calories) {
        if (calories < 40) return 'red'
        else if (calories < 100) return 'orange'
        else return 'green'
      },
      validate () {
        this.$refs.form.validate()
      },
      reset () {
        this.$refs.form.reset()
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },

      initialize () {
        this.desserts = [
          { name: 'Frozen Yogurt', category: 6.0, price: 'Rp 12.000', hpp: 'Rp 10.000', },
          { name: 'Ice cream sandwich', category: 9.0, price: 'Rp 20.000', hpp: 'Rp 12.000', },
          { name: 'Eclair', category: 16.0, price: 'Rp 23.000', hpp: 'Rp 20.000', },
          { name: 'Cupcake', category: 3.7, price: 'Rp 90.000', hpp: 'Rp 82.000', },
          { name: 'Gingerbread', category: 16.0, price: 'Rp 45.000', hpp: 'Rp 32.000', },
          { name: 'Jelly bean', category: 0.0, price: 'Rp 43.000', hpp: 'Rp 39.000', },
          { name: 'Lollipop', category: 0.2, price: 'Rp 67.000', hpp: 'Rp 62.000', },
          { name: 'Honeycomb', category: 3.2, price: 'Rp 55.000', hpp: 'Rp 45.000', },
          { name: 'Donut', category: 25.0, price: 'Rp 89.000', hpp: 'Rp 79.000', },
          { name: 'KitKat', category: 26.0, price: 'Rp 78.000', hpp: 'Rp 70.000', },
        ]
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      deleteItemConfirm () {
        this.desserts.splice(this.editedIndex, 1)
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>