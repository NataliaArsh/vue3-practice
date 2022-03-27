<template>
  <div>
    <div v-if="posts.length > 0">
      <h3>Список постов</h3>
      <post-item
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
      /> 
    </div>
    <h2 v-else>Список постов пуст</h2>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  components: {
    PostItem
  },
  props: {
    posts: {
      type: Array,
      recuired: true
    }
  }
}
</script>


<style scoped>
h2 {
  color: rgba(102, 51, 153, 0.555);
}
</style>
