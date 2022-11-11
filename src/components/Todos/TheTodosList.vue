<template>
<div class="p-6 w-full bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700 my-5">
    <h2 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Todos:</h2>
    
    <label for="countries" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Selecione a Quantidade de Registro a Serem Exibidos</label>
    <select @change="changeLimitSearch()" v-model="limit" id="countries" class="mb-3 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
        <option selected value="">Selecione</option>
        <option value="5">5</option>
        <option value="10">10</option>
        <option value="15">15</option>
        <option value="20">20</option>
        <option value="30">30</option>
    </select>

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
                limit: '',
            }
        },
        created() {
            this.getAllTodoslist()
        },
        
        methods: {
            changeLimitSearch(){
                this.getAllTodoslist()
            },
            getAllTodoslist(){
                axios({
                    method: 'GET',
                    url: 'https://jsonplaceholder.typicode.com/todos',
                    params:{
                        _limit: this.limit != '' ? this.limit : 5,
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