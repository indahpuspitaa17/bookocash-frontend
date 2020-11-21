<template>
    <v-container>
        <v-row>
        <template>
            <v-col  
            v-for="item in summary"
            :key="item"
            cols="24"
            sm="3">
                <v-card color="#363062" dark class="pa-5">
                    <v-list-item>
                        <v-list-item-content>
                            <v-list-item-title 
                                class="headline font-weight-black"
                                >{{ item.price }}
                            </v-list-item-title>
                            <v-divider></v-divider>
                            <v-list-item-subtitle 
                                class="body-2 text-capitalize"
                                >{{ item.name }}
                            </v-list-item-subtitle>
                        </v-list-item-content>
                    </v-list-item>
                </v-card>
            </v-col>
        </template>
        </v-row>
    </v-container>
</template>

<script>
export default {
    head() {
    return {
      title: 'Dashboard',
      script: [
        {src:'/dashboard.js'}
      ]
    }
    },
    data() {
        return {
            summary: [
                {name: 'Total Income', price: '13.000'},
                {name: 'Total Customer', price: '14'},
                {name: 'Total Sales', price: '15.000'},
                {name: 'Total Product', price: '19.000'}
            ]
        }
    },
    summary: [],
    
}
</script>