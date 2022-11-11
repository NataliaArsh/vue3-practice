<template>
    <div class="post">
      <div>
        <div>{{ post.id }}</div>
        <div class="post__title"><strong>Название:</strong> {{ post.title }}</div>
        <div class="post__body"><strong>Описание:</strong> {{ post.body }}</div>
      </div>
      <my-button
        class="post__btn"
        @click="$emit('remove', post)"
      >
        Удалить
      </my-button>
    </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      recuired: true
    }
  },
}
</script>


<style scoped>
.post {
  border: 2px solid rgb(219, 116, 219);
  margin: 10px 0;
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

.post__title {
  margin-bottom: 5px;
}
.post__btn{
  align-self: center;
  margin-left: 10px;
}
</style>
