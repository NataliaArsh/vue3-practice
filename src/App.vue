<template>
  <div class="app">
    <my-button
      class="btn-dialog" @click="showDialog"
    >
      Создать пост 
    </my-button>
    <my-button @click="fetchPosts">
      Загрузить посты
    </my-button>
    <my-dialog v-model:show="visibleDialog">
      <post-form
        @add="addPost"
      />
    </my-dialog>
    <post-list 
      :posts="posts"
      @remove="removePost"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from './components/UI/MyDialog.vue';
import MyButton from './components/UI/MyButton.vue';
import axios from 'axios';
export default {
  components: {
    PostForm, 
    PostList,
    MyDialog,
    MyButton,
  },
  data() {
    return {
      posts: [],
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
    async fetchPosts() {
      try {
        const respons = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = respons.data;
      } catch(e) {
        alert('Ошибка')
      }
    },
  },
}
</script>


<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
  padding: 15px;
}

h3 {
  margin-bottom: 10px;
  color: rebeccapurple;
}

.btn-dialog {
  margin: 15px 0;
}
</style>
