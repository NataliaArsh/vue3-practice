<template>
    <div>
        <my-input 
            v-model="searchQuery" 
            placeholder="Поиск..." 
            v-focus
        />
        <div class="app__btn">
            <my-button 
                @click="showDialog"
            >
                Создать пост
            </my-button>
            <my-select 
                v-model="selectedSort" 
                :options="sortOptions" 
            />
        </div>
        <my-dialog 
            v-model:show="visibleDialog"
        >
            <post-form/>
        </my-dialog>
        <post-list 
            v-if="!isPostsLoading" 
            :posts="sortedAndReserchedPosts"
        />
        <div v-else>Идет загрузка..</div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import usePosts from '@/hooks/usePosts';
import useSortedPosts from '@/hooks/useSortedPosts';
import useSortedAndSearchedPosts from '@/hooks/useSortedAndSearchedPosts';
export default {
    components: {
        PostForm,
        PostList,
    },
    data() {
        return {
            visibleDialog: false,
            sortOptions: [
                { value: 'title', name: ' По названию' },
                { value: 'body', name: ' По описанию' },
            ]
        }
    },
    setup(props) {
        const { posts, isPostsLoading, totalPages } = usePosts(10)
        const { selectedSort, sortedPosts } = useSortedPosts(posts)
        const { searchQuery, sortedAndReserchedPosts } = useSortedAndSearchedPosts(sortedPosts)

    return {
        posts, 
        isPostsLoading, 
        totalPages,
        selectedSort,
        sortedPosts,
        searchQuery, 
        sortedAndReserchedPosts 
    }
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
