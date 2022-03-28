<template>
  <div class="app">
    <my-button
      class="btn-dialog" @click="showDialog"
    >
      Создать
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
export default {
  components: {
    PostForm, 
    PostList,
    MyDialog,
    MyButton,
  },
  data() {
    return {
      posts: [
        {id:1, title: 'какое-то название 1', body: 'какое-то описание 1'},
        {id:2, title: 'какое-то название 2', body: 'какое-то описание 2'},
        {id:3, title: 'какое-то название 3', body: 'какое-то описание 3'},
      ],
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
