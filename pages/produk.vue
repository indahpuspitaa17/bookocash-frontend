<template>
    <v-container>
        <v-row>
            <v-col
            v-for="n in 2"
            :key="n"
            cols="12"
            sm="4"
            >
                <v-card>
                    <v-card-title>
                    haindah
                    </v-card-title>
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
      script: [
        {src:'/produk.js'}
      ]
    }
  },
}
</script>