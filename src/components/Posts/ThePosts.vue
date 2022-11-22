<template>
    <section class="my-4 flex items-center justify-between">
        <h2 class=" text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Publicações <span class="text-blue-900">({{totalPost}})</span> </h2>
        <div class="filter flex flex-col  justify-start items-center">
            <h2 class=" text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Filtros/Ações</h2>
            
            <div class="content-filter mt-5 flex">
                
                <div class="button-create-new-post self-end" >
                    <button type="button" @click="showModalCreateNewPost" class="text-white bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none
                     focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Criar novo post</button>
                </div>


                <div class="filter-limit-result-request">
                <select id="limit-request" v-model="limit"
                    class="w-36 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5
                     dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                    <option value="">Select an post</option>
                    <option value="5">5</option>
                    <option value="10">10</option>
                    <option value="15">10</option>
                    <option value="20">20</option>
                    <option value="all">Todos</option>
                </select>

                </div>
                <div class="filter-limit-result-request ml-3">
                <select id="limit-request"  v-model="post_id"
                    class="w-36 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5
                     dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                     <option value="">Select an Publication</option>
                    <option v-for="post in posts" :key="post.id" :value="post.id">{{post.title}}</option>
                </select>

                </div>
            </div>
        </div>
    </section>


    <div v-for="post in posts" :key="post.id">
        <PostVue  v-bind:post="post" @getPost="getPost"/>
    </div>
   
    <!-- Modal Register new Post -->
    <Modal v-show="isModalVisible" @close="closeModal">
        <template v-slot:header>
            <h1>Register new post</h1>
        </template>
        <template v-slot:body>
            <form @submit.prevent="register()">
                <div class="mb-6">
                    <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Title</label>
                    <input type="text" id="email"
                        v-model="form.title"
                        class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
                        placeholder="Title.." required>
                </div>
        
                <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Description</label>
                <textarea id="message" rows="4"
                    v-model="form.description"
                    class="mb-4 block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Description..."></textarea>
        
                <button type="submit"
                    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Register
                    new post</button>
            </form>
        </template>
    </Modal>
    <!-- Modal Update Post -->
    <Modal v-show="isModalUpdatePostVisible" @close="closeModal" v-if="post[0] != null">
        <template v-slot:header>
            <h1>Update Post</h1>
        </template>
        <template v-slot:body>
            <pre>
                
            </pre>
            <form @submit.prevent="register()">
                <div class="mb-6">
                    <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Title</label>
                    <input type="text" id="email"
                        
                        class="shadow-sm capitalize bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
                        placeholder="Title.." :value="post[0].title">
                </div>
        
                <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Description</label>
                <textarea id="message" rows="4"
                    
                    class="mb-4 block capitalize p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Description..." :value="post[0].body"></textarea>
        
                <button type="submit"
                    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Update Post</button>
            </form>
        </template>
    </Modal>

</template>
<script>

import PostVue from './ThePostElement.vue'
import Modal from '../Modal.vue';

import axios from 'axios'
export default {
    
    components: {
        PostVue,
        Modal
    },
    data() {
        return {

            posts: Object,
            post: Object,
            limit: '',
            post_id: '',
            isModalVisible: false,
            isModalUpdatePostVisible: false,
            form:{
                title: '',
                description: ''
            }

        }
    },
    created() {
        this.getAllPosts()

    },
    watch: {

        limit(newValue) {

            this.getAllPosts(newValue);
        },
        post_id(newValue) {

            this.filterPost(newValue)
        }
    },
    computed: {
        totalPost() {
            return this.posts.length;
        }
    },
    methods: {
        getAllPosts(value) {

            const limit = (value == '') ? 5 : (value == 'all') ? '' : value

            axios({
                method: 'GET',
                url: 'https://jsonplaceholder.typicode.com/posts',
                params: {
                    _limit: this.limit != '' ? limit : 5,
                }
            }).then((response) => {
                this.posts = response.data
            }).catch((error) => {

                console.log(error.response.data);
            })
        },
        getPost(id) {
            
            if(id != null){

                this.post = this.posts.filter(post => post.id == id)
                this.isModalUpdatePostVisible = true;
                console.log(this.post[0].title)
            }
          

        },
        filterPost(id) {
            
            if(id != null){

                this.post = this.posts.filter(post => post.id == id)
                this.isModalUpdatePostVisible = true;
                console.log(this.post[0].title)
            }
          

        },
        showModalCreateNewPost(){
            this.isModalVisible = true;
        },
        closeModal() {
            this.isModalVisible = false;
            this.isModalUpdatePostVisible = false;
        },
        register() {
            
            this.form.append('userId', 2);
            console.log('form', this.form)
            axios({
                method: 'POST',
                url: 'https://jsonplaceholder.typicode.com/posts',
                body:  JSON.stringify({
                    title: 'foo',
                    body: 'bar',
                    userId: 2,
                }),
                headers:{
                    'Content-type': 'application/json; charset=UTF-8',
                }
            }).then((response) =>{

                console.log('response', response.data)

            }).catch((error) =>{

                console.log('error', error.response.data)
            })
        }
        

    },

}
</script>