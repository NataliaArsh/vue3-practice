<template>
  <div class="app">
    <post-form
      @add="addPost"
    />
    <post-list 
      :posts="posts"
      @remove="removePost"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
export default {
  components: {
    PostForm, PostList
  },
  data() {
    return {
      posts: [
        {id:1, title: 'какое-то название 1', body: 'какое-то описание 1'},
        {id:2, title: 'какое-то название 2', body: 'какое-то описание 2'},
        {id:3, title: 'какое-то название 3', body: 'какое-то описание 3'},
      ],
    }
  },
  methods: {
    addPost(post) {
      this.posts.push(post)
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    }

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
</style>
