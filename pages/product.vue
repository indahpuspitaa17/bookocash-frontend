<template>
  <v-container>
    <v-row cols="12" mt="4">
      <v-col>
        <h2>Daftar <strong>Makanan</strong></h2>
      </v-col>
    </v-row>

    <v-row col="12" mt="4">
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
              <v-icon> mdi-magnify </v-icon>
            </span>
          </div>
        </div>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="24" sm="3" v-for="product in products" :key="product.id">
        <add-product :product="product" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  head() {
    return {
      title: "Product",
    };
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    getAllProducts() {
      // get all product ke backend
      // kalo backend nya udah bisa disambunging
      this.$axios
        .get("/products")
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log(error));
    },
    getDummyProducts() {
      const available = [
        {
          nama: "Bakso Urat",
          gambar: "/images/bakso.jpg",
        },
        {
          nama: "Kentang Goreng",
          gambar: "/images/kentang-goreng.jpg",
        },
        {
          nama: "Lontong Opor Ayam",
          gambar: "/images/lontong-opor-ayam.jpg",
        },
        {
          nama: "Mie Ayam Bakso",
          gambar: "/images/mie-ayam-bakso.jpg",
        },
        {
          nama: "Mie Goreng",
          gambar: "/images/mie-goreng.jpg",
        },
        {
          nama: "Nasi Ayam Geprek",
          gambar: "/images/nasi-ayam-geprek.jpg",
        },
      ];

      const data = available.map((item) => ({
        ...item,
        harga: this.getRandomInt(100000),
        stock: this.getRandomInt(20),
      }));

      this.setProducts(data);
    },
    getRandomInt(max) {
      return Math.floor(Math.random() * Math.floor(max));
    },
    searchFood() {},
  },
  mounted() {
    this.getDummyProducts();
  },
};
</script>
<style>
</style>
