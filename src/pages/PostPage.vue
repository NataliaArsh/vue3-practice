<template>
    <div>
        <my-input 
            v-model="searchQuery" 
            placeholder="Поиск..." 
            v-focus
        />
        <div class="app__btn">
            <my-button @click="showDialog">
                Создать пост
            </my-button>
            <my-select v-model="selectedSort" :options="sortOptions" />
        </div>
        <my-dialog v-model:show="visibleDialog">
            <post-form @add="addPost" />
        </my-dialog>
        <post-list v-if="!isPostsLoading" :posts="sortedAndReserchedPosts" @remove="removePost" />
        <div v-else>Идет загрузка..</div>
        <div v-intersection="loadMorePosts" class="observer"></div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';
export default {
    components: {
        PostForm,
        PostList,
    },
    data() {
        return {
            posts: [],
            visibleDialog: false,
            isPostsLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                { value: 'title', name: ' По названию' },
                { value: 'body', name: ' По описанию' },
            ]
        }
    },
    methods: {
        addPost(post) {
            this.posts.push(post);
            this.visibleDialog = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
        },
        showDialog() {
            this.visibleDialog = true;
        },
        async fetchPosts() { // это ф-я подгрузки постов
            try {
                this.isPostsLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = response.data;
            } catch (e) {
                alert('Ошибка')
            } finally {
                this.isPostsLoading = false;
            }
        },
        async loadMorePosts() { // это ф-я подгрузки новых постов
            try {
                this.page += 1;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = [...this.posts, ...response.data];
            } catch (e) {
                alert('Ошибка')
            }
        },
    },
    mounted() {
        this.fetchPosts();
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },
        sortedAndReserchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },
    watch: {
        //selectedSort(newValue) {
        //this.posts.sort((post1, post2) => {
        //return post1[newValue]?.localeCompare(post2[newValue])
        //})
    }
}
</script>


<style>
.app__btn {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
}

.page__wrapper {
    display: flex;
    margin-top: 15px;
}

.page {
    border: 1px solid black;
    padding: 10px;
}

.current-page {
    border: 2px solid rgb(219, 116, 219);
}

.observer {
    height: 30px;
    background-color: rgb(213, 150, 213);
}
</style>
