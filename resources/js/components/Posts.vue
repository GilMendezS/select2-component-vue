<template>
    <div>
        <p>Selected: {{selected}}</p>
        <select2 :default_option="title" @input="changeValue" :options="posts">
            <option disabled value="0">Select one post</option>
        </select2>
        <button :disabled="!selected">send</button>
    </div>
</template>
<script>
import axios from 'axios'
import CustomSelect from './CustomSelect.vue'
export default {
    components: {
        'select2': CustomSelect
    },
    data(){
        return {
            posts:[],
            selected: '',
            title: 'Select an option'
        }
    },
    created(){
        axios.get('https://jsonplaceholder.typicode.com/posts')
        .then(response => {
            this.posts = response.data.map(item => {
                return {id: item.id , text: `${item.title}`}
            })
        })
        .catch(err => {

        })
        .finally(() => {

        })
    },
    methods : {
        changeValue(value){
            this.selected = value
        }
    }
}
</script>

