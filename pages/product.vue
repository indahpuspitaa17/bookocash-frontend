<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    class="elevation-1"
  > 

    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title class="font-weight-bold">Product List</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="1000px"
        >
          <!-- ADD PRODUCT -->
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="#363062" 
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              Add Product
            </v-btn>
          </template>

          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>
            <v-row>
              <!-- PRODUCT DETAILS -->
              <v-col>
                <v-card-text>
                  <v-container>
                    <div>
                      Product Details
                    </div>
                    <v-row>
                      <v-col
                        cols="12"
                        sm="6"
                        md="6"
                      >
                        <v-text-field
                          v-model="editedItem.product_name"
                          label="Product"
                          :rules="[v => !!v || 'Product is required']"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col
                        cols="12"
                        sm="6"
                        md="6"
                      >
                        <v-select
                          v-model="category"
                          :items="category"
                          :rules="[v => !!v || 'Category is required']"
                          label="Category"
                          required
                        ></v-select>
                      </v-col>
                      <v-col
                        cols="12"
                        sm="6"
                        md="6"
                      >
                        <v-text-field
                          v-model="editedItem.price"
                          label="Price"
                          :rules="[v => !!v || 'Price is required']"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col
                        cols="12"
                        sm="6"
                        md="6"
                      >
                        <v-text-field
                          v-model="editedItem.hpp"
                          label="HPP"
                          :rules="[v => !!v || 'HPP is required']"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col>
                        <v-file-input
                          label="Click to upload product picture"
                          filled
                          prepend-icon="mdi-camera"
                        ></v-file-input>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>
              </v-col>

              <!-- INGREDIENTS -->
              <v-col>
                <v-card-text>
                  <v-container>
                    <div>
                      Ingridients
                    </div>
                    <v-row >
                      <v-col
                        cols="12"
                        sm="6"
                        md="12">
                        <v-btn 
                          color="#827397" 
                          dark
                          @click="addIngridient"> ADD 
                        </v-btn>
                      </v-col>
                      
                      <v-col>
                        <v-row
                          v-for="(add, index) in adds"
                          :key="add"
                        >
                          <v-col
                          cols="12"
                          sm="3"
                          md="3"
                          >
                            <v-text-field
                              v-model="add.ingridients"
                              label="Ingridients"
                              :rules="[v => !!v || 'Ingridients is required']"
                              required
                            ></v-text-field>
                          </v-col>

                          <v-col
                          cols="12"
                          sm="3"
                          md="3"
                          >
                            <v-text-field
                              v-model="add.amount"
                              label="Amount"
                              :rules="[v => !!v || 'Amount is required']"
                              required
                            ></v-text-field>
                          </v-col>

                          <v-col
                          cols="12"
                          sm="3"
                          md="3"
                          >
                            <v-text-field
                              v-model="add.unit"
                              label="Unit"
                              :rules="[v => !!v || 'Unit is required']"
                              required
                            ></v-text-field>
                          </v-col>

                          <v-col
                          cols="12"
                          sm="3"
                          md="3">
                            <span 
                              class="float-right" 
                              style="cursor:pointer"
                              @click="deleteIngridient(index)">
                                <v-icon>mdi-close</v-icon>
                            </span>
                          </v-col>
                        </v-row>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>
              </v-col>
            </v-row>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="red darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

        <!-- DIALOG HAPUS -->
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="headline">Are you sure you want to delete this item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="red darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
</template>

<script>
  export default {
    head() {
    return {
      title: 'Product',
      }
    },
    data: () => ({
      dialog: false,
      dialogDelete: false,
      select: null,
      adds: [
        {
          ingridients: '',
          amount: '',
          unit: ''
        }
      ],
      category: [
        'Food',
        'Beverage',
        'Dessert',
      ],
      headers: [
        { text: 'Product', align: 'start', sortable: false,value: 'product_name', },
        { text: 'Category', value: 'category' },
        { text: 'Selling Price', value: 'price' },
        { text: 'HPP', value: 'hpp' },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        product_name: '',
        category: [
          'Food'||
          'Beverage'||
          'Dessert'
        ],
        price: '',
        hpp: '',
      },
      defaultItem: {
        product_name: '',
        category: [
          'Food'||
          'Beverage'||
          'Dessert',
        ],
        price: '',
        hpp: '',
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      addIngridient () {
        this.adds.push({
          ingridients: '',
          amount: '',
          unit: ''
        })
      },
      deleteIngridient (index) {
        this.adds.splice(index, 1)
      },
      initialize () {
        this.desserts = [
          { product_name: 'Frozen Yogurt', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 12.000', hpp: 'Rp 10.000', },
          { product_name: 'Ice cream sandwich', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 20.000', hpp: 'Rp 12.000', },
          { product_name: 'Eclair', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 23.000', hpp: 'Rp 20.000', },
          { product_name: 'Cupcake', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 90.000', hpp: 'Rp 82.000', },
          { product_name: 'Gingerbread', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 45.000', hpp: 'Rp 32.000', },
          { product_name: 'Jelly bean', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 43.000', hpp: 'Rp 39.000', },
          { product_name: 'Lollipop', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 67.000', hpp: 'Rp 62.000', },
          { product_name: 'Honeycomb', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 55.000', hpp: 'Rp 45.000', },
          { product_name: 'Donut', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 89.000', hpp: 'Rp 79.000', },
          { product_name: 'KitKat', category: ['Food'|| 'Beverage' || 'Dessert'], price: 'Rp 78.000', hpp: 'Rp 70.000', },
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