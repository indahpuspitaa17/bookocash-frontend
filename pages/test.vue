<template>
    <v-text-field v-model="name" 
    label="Nama"
    @change="print()">
        
    </v-text-field>
</template>

<script>
export default {
    data() {
        return {
            name: 'indah',
            post: []
        }
    },
    methods: {
        print() {
            console.log(this.name)
        },
        getPost() {
            this.$axios.$get('https://jsonplaceholder.typicode.com/posts').then((response) => {
                console.log(response)
            })
        }
    },
    mounted() {
        this.getPost()
    }
}
</script>