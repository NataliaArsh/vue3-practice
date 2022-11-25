<template>
    <div>
        <my-input 
            :model-value="searchQuery" 
            @update:model-value="setSearchQuery"
            placeholder="Поиск..." 
            v-focus
        />
        <div class="app__btn">
            <my-button @click="showDialog">
                Создать пост
            </my-button>
            <my-select 
                :model-value="selectedSort" 
                @update:model-value="setSelectedSort"
                :options="sortOptions" 
            />
        </div>
        <my-dialog v-model:show="visibleDialog">
            <post-form @add="addPost" />
        </my-dialog>
        <post-list 
            v-if="!isPostsLoading" 
            :posts="sortedAndReserchedPosts" 
            @remove="removePost" 
        />
        <div v-else>Идет загрузка..</div>
        <div v-intersection="loadMorePosts" class="observer"></div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import {mapActions, mapGetters, mapState, mapMutations} from 'vuex';
export default {
    components: {
        PostForm,
        PostList,
    },
    data() {
        return {
            visibleDialog: false,
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
        ...mapMutations({
            setPage: 'post/setPage',
            setSearchQuery: 'post/setSearchQuery',
            setSelectedSort: 'post/setSelectedSort'
        }),
        ...mapActions({
            fetchPosts: 'post/fetchPosts',
            loadMorePosts: 'post/loadMorePosts'
        })
    },
    mounted() {
        this.fetchPosts();
    },
    computed: {
        ...mapState({
            posts: state => state.post.posts,
            isPostsLoading: state => state.post.isPostsLoading,
            selectedSort: state => state.post.selectedSort,
            searchQuery: state => state.post.searchQuery,
            page: state => state.post.page,
            limit: state => state.post.limit,
            totalPages: state => state.post.totalPages,
            sortOptions: state => state.post.sortOptions,
        }),
        ...mapGetters({
            sortedPosts: 'post/sortedPosts',
            sortedAndReserchedPosts: 'post/sortedAndReserchedPosts' 
        })
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
