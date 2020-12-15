<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    sort-by="orderId"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar flat>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="#363062" dark class="mb-2" v-bind="attrs" v-on="on">
              Add Order
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
                      v-model="editedItem.nameCustomer"
                      label="Customer name"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.orderType"
                      label="Order type"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.tableNumber"
                      label="Table number"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.cashier"
                      label="Cashier in Charge"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.satus"
                      label="Status"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close"> Cancel </v-btn>
              <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="headline"
              >Are you sure you want to delete this item?</v-card-title
            >
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete"
                >Cancel</v-btn
              >
              <v-btn color="blue darken-1" text @click="deleteItemConfirm"
                >OK</v-btn
              >
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:[`item.actions`]="{ item }">
      <v-icon small @click="detailItem(item)"> mdi-library-books </v-icon>
      <v-icon small @click="editItem(item)"> mdi-pencil </v-icon>
      <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize"> Reset </v-btn>
    </template>
  </v-data-table>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      { text: "Order Id", align: "start", sortable: true, value: "orderId" },
      { text: "Customer Name", value: "nameCustomer" },
      { text: "Order Type", value: "orderType" },
      { text: "Table Number", value: "tableNumber" },
      { text: "Cashier", value: "cashier" },
      { text: "Status", value: "status" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
    detailItem: {
      orderId: "",
      nameCustomer: "",
      orderType: "",
      tableNumber: "",
      cashier: "",
      status: "",
    },
    editedItem: {
      orderId: "",
      nameCustomer: "",
      orderType: "",
      tableNumber: "",
      cashier: "",
      status: "",
    },
    defaultItem: {
      orderId: "",
      nameCustomer: "",
      orderType: "",
      tableNumber: "",
      cashier: "",
      status: "",
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
    initialize() {
      this.desserts = [
        {
          orderId: "#001",
          nameCustomer: "Ahmad",
          orderType: "Dine-in",
          tableNumber: 6,
          cashier: "Bambang",
          status: "In process",
        },
        {
          orderId: "#002",
          nameCustomer: "Banjaran",
          orderType: "Dine-in",
          tableNumber: 2,
          cashier: "Bambang",
          status: "In process",
        },
        {
          orderId: "#003",
          nameCustomer: "Bob",
          orderType: "Dine-in",
          tableNumber: 4,
          cashier: "Bambang",
          status: "In process",
        },
        {
          orderId: "#004",
          nameCustomer: "Yuwono",
          orderType: "Dine-in",
          tableNumber: 1,
          cashier: "Bambang",
          status: "In process",
        },
        {
          orderId: "#005",
          nameCustomer: "Aan",
          orderType: "Dine-in",
          tableNumber: 7,
          cashier: "Bambang",
          status: "In process",
        },
        {
          orderId: "#006",
          nameCustomer: "Indah",
          orderType: "Dine-in",
          tableNumber: 9,
          cashier: "Bambang",
          status: "In process",
        },
        {
          orderId: "#007",
          nameCustomer: "Fadia",
          orderType: "Take-away",
          tableNumber: "-",
          cashier: "Bambang",
          status: "In process",
        },
        {
          orderId: "#008",
          nameCustomer: "Ahmad",
          orderType: "Take-away",
          tableNumber: "-",
          cashier: "Bambang",
          status: "In process",
        },
      ];
    },

    //Nanti edit lagi, belum ada page menu pembelian euy
    detailItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
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