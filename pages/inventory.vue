<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    sort-by="stock"
    class="elevation-1"
  >
    <template v-slot:[`item.stock`]="{ item }">
      <v-chip :color="getColor(item.stock)" dark>
        {{ item.stock }}
      </v-chip>
    </template>

    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>Inventory</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="#363062" dark class="mb-2" v-bind="attrs" v-on="on">
              Add Stock
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.name"
                      label="Ingridients"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.stock"
                      label="Stock"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      v-model="editedItem.date"
                      :close-on-content-click="false"
                      :nudge-right="40"
                      transition="scale-transition"
                      offset-y
                      min-width="290px"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="date"
                          label="Date"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="date"
                        @input="editedItem.date = false"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.amount"
                      label="Amount"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="red darken-1" text @click="close"> Cancel </v-btn>
              <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="headline">
              Are you sure you want to delete this item?
            </v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">
                Cancel
              </v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">
                OK
              </v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:[`item.actions`]="{ item }">
      <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
      <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize"> Reset </v-btn>
    </template>
  </v-data-table>
</template>

<script>
export default {
  head() {
    return {
      title: "Inventory",
    };
  },
  data: () => ({
    date: new Date().toISOString().substr(0, 10),
    modal: false,
    dialog: false,
    dialogDelete: false,
    headers: [
      { text: "Ingredients", align: "start", sortable: false, value: "name" },
      { text: "Amount", value: "amount" },
      { text: "Last Update", value: "date" },
      { text: "Stock", value: "stock" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      stock: "",
      date: "",
      amount: "",
    },
    defaultItem: {
      name: "",
      stock: "",
      date: "",
      amount: "",
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    getColor(stock) {
      if (stock < 40) return "red";
      else if (stock < 100) return "orange";
      else return "green";
    },
    initialize() {
      this.desserts = [
        { name: "Frozen Yogurt", stock: 159, date: "", amount: 24 },
        { name: "Ice cream sandwich", stock: 237, date: 9.0, amount: 37 },
        { name: "Eclair", stock: 62, date: 16.0, amount: 23 },
        { name: "Cupcake", stock: 30, date: 3.7, amount: 67 },
        { name: "Gingerbread", stock: 56, date: 16.0, amount: 49 },
        { name: "Jelly bean", stock: 75, date: 0.0, amount: 94 },
        { name: "Lollipop", stock: 92, date: 0.2, amount: 98 },
        { name: "Honeycomb", stock: 408, date: 3.2, amount: 87 },
        { name: "Donut", stock: 452, date: 25.0, amount: 51 },
        { name: "KitKat", stock: 518, date: 26.0, amount: 65 },
      ];
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.desserts.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
      } else {
        this.desserts.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>