<template>
<div class="p-6 w-full bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700 my-5">
    <h2 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Todos:</h2>
    <ul class="space-y-1 max-w-md list-inside text-gray-500 dark:text-gray-400">
        <li class="flex items-center" v-for="todo in todos" :key="todo.id">
            <svg v-if="todo.completed" class="w-4 h-4 mr-1.5 text-green-500 dark:text-green-400 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>
            <svg v-if="!todo.completed" class="w-4 h-4 mr-1.5 text-gray-400 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg>
        {{todo.title}}
        </li>
        
        <li class="flex items-center hidden">
            <svg class="w-4 h-4 mr-1.5 text-gray-400 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg>
            At least one special character, e.g., ! @ # ?
        </li>
    </ul>
</div>
</template>
<script>
    import axios from 'axios'
    export default{
        data(){
            return{

                todos: Object,
            }
        },
        created() {
            this.getAllTodoslist()
        },
        methods: {
            getAllTodoslist(){
                axios({
                    method: 'GET',
                    url: 'https://jsonplaceholder.typicode.com/todos',
                    params:{
                        _limit: 10,
                    }
                }).then((response) =>{
                    this.todos = response.data
                }).catch((error) =>{
                    
                    console.log(error.response.data);
                })
            }
        },
    }
</script>