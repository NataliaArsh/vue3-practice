<template>
    <div class="post">
        <div class="post__title"><strong>Название:</strong> {{ post.title }}</div>
        <div class="post__body"><strong>Описание:</strong> {{ post.body }}</div>
    </div>
</template>

<script>
export default {
    props: {
      post: {
        type: Object,
        recuired: true
      }
    }
}
</script>


<style scoped>
.post {
  border: 2px solid rgb(224, 87, 224);
  margin: 10px 0;
  padding: 10px;
}

.post__title {
  margin-bottom: 5px;
}
</style>
