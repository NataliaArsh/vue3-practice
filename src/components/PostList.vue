<template>
  <div>
    <div v-if="posts.length > 0">
      <h2>Список постов</h2>
      <transition-group name="post-list">
        <post-item 
          v-for="post in posts" 
          :post="post" 
          :key="post.id" 
          @remove="$emit('remove', post)" 
        />
      </transition-group>
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

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}

.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.5s ease;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.post-list-move {
  transition: transform 0.5s ease;
}
</style>
