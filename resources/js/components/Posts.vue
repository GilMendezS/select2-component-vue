<template>
    <div>
        <p>Selected: {{selected}}</p>
        <select2 :default_option="title" 
            extra_classes="form-control"
            @input="changeValue" :options="posts">
            <option disabled value="0">Select one post</option>
        </select2>
        <button @click="reloadData" :disabled="!selected">send</button>
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
            console.log(response.data)
            this.posts = response.data.map(item => {
                return {id: item.id , text: `${item.id} - ${item.title}`}
            })
        })
        .catch(err => {

        })
        .finally(() => {

        })
    },
    methods : {
        reloadData(){
            axios.get('https://jsonplaceholder.typicode.com/users')
        .then(response => {
            this.selected = ''
            this.posts = response.data.map(item => {
                return {id: item.id , text: `${item.id} - ${item.name}`}
            })
            
        })
        .catch(err => {

        })
        .finally(() => {

        })
        },
        changeValue(value){
            this.selected = value
        }
    }
}
</script>

