<template>
  <v-container>
    <v-row 
      cols="12"
      mt="4">
      <v-col>
        <h2> Daftar <strong>Makanan</strong></h2>
      </v-col>
    </v-row>

    <v-row 
      col="12"
      mt="4">
      <v-col>
        <div class="input-group mb-3">
          <input
            v-model="search"
            type="text"
            class="form-control"
            placeholder="Cari Makanan Kesukaan Anda .."
            aria-label="Cari"
            aria-describedby="basic-addon1"
            @keyup="searchFood"
          />
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">
              <b-icon-search></b-icon-search>
            </span>
          </div>
        </div>
      </v-col>
    </v-row>

    <v-row>
      <v-col
        cols="24"
        sm="3"
        v-for="product in products"
        :key="product.id">
          <AddProduct :product="product" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import AddProduct from '../components/product/AddProduct'
import axios from "axios";
export default {
  name: "food",
  components: {
    AddProduct
  },
  data() {
    return {
      products: [],
      search: '',
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchFood() {
      axios
      .get("http://localhost:3333/products?q="+this.search)
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
    }
  },
  mounted() {
    axios
      .get("http://localhost:3333/products")
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
<style>
</style>
