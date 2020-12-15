<template>
  <v-card class="mx-auto my-12">
    <img
      v-bind:src="'../assets/images/' + product.gambar"
      class="card-img-top"
      alt="..."
    />

    <v-card-title> {{ product.nama }} </v-card-title>
    <v-card-text>
      <v-col>
        <v-row> Harga : Rp. {{ product.harga }} </v-row>
        <v-row>
          <v-btn color="success" class="mr-4"> Pesan </v-btn>
        </v-row>
      </v-col>
    </v-card-text>
  </v-card>
</template>
<!-- 
<template>
  <div class="card shadow card-product">
    <img v-bind:src=" '../assets/images/' + product.gambar " class="card-img-top" alt="..." />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <p
        class="card-text"
      >Harga : Rp. {{ product.harga }}</p>
      <router-link class="btn btn-success" :to="'/foods/'+product.id"> Tambahkan </router-link>
    </div>
  </div>
</template> -->

<script>
export default {
  props: ["product"],
};
</script>

<style>
</style>
