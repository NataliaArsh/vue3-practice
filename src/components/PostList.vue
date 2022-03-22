<template>
  <div>
    <h3>Список постов</h3>
    <post-item
      v-for="post in posts"
      :post="post"
    /> 
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

</style>
