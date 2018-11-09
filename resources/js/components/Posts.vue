<template>
    <div>
        
    </div>
</template>
<script>
import axios from 'axios'
import CustomSelect from './CustomSelect.vue'
export default {
    components: {
        'sellect2': CustomSelect
    },
    data(){
        return {
            posts:[]
        }
    },
    mounted(){
        axios.get('https://jsonplaceholder.typicode.com/posts')
        .then(response => {
            this.posts = response.data
        })
        .catch(err => {

        })
        .finally(() => {

        })
    }
}
</script>

