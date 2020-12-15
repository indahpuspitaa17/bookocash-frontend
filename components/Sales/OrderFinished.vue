<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    sort-by="orderId"
    class="elevation-1"
  >
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
    ],
    desserts: [],
    editedIndex: -1,
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
          status: "Finished",
        },
        {
          orderId: "#002",
          nameCustomer: "Banjaran",
          orderType: "Dine-in",
          tableNumber: 2,
          cashier: "Bambang",
          status: "Finished",
        },
        {
          orderId: "#003",
          nameCustomer: "Bob",
          orderType: "Dine-in",
          tableNumber: 4,
          cashier: "Bambang",
          status: "Finished",
        },
        {
          orderId: "#004",
          nameCustomer: "Yuwono",
          orderType: "Dine-in",
          tableNumber: 1,
          cashier: "Bambang",
          status: "Finished",
        },
        {
          orderId: "#005",
          nameCustomer: "Aan",
          orderType: "Dine-in",
          tableNumber: 7,
          cashier: "Bambang",
          status: "Finished",
        },
        {
          orderId: "#006",
          nameCustomer: "Indah",
          orderType: "Dine-in",
          tableNumber: 9,
          cashier: "Bambang",
          status: "Finished",
        },
        {
          orderId: "#007",
          nameCustomer: "Fadia",
          orderType: "Take-away",
          tableNumber: "-",
          cashier: "Bambang",
          status: "Finished",
        },
        {
          orderId: "#008",
          nameCustomer: "Ahmad",
          orderType: "Take-away",
          tableNumber: "-",
          cashier: "Bambang",
          status: "Finished",
        },
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