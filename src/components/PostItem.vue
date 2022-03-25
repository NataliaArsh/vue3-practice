<template>
    <div class="post">
      <div>
        <div class="post__title"><strong>Название:</strong> {{ post.title }}</div>
        <div class="post__body"><strong>Описание:</strong> {{ post.body }}</div>
      </div>
      <my-button
      class="post__btn"
      >
        Удалить
      </my-button>
    </div>
</template>

<script>
import MyButton from './UI/MyButton.vue'
export default {
  components: { MyButton },
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
  display: flex;
  justify-content: space-between;
}

.post__title {
  margin-bottom: 5px;
}
.post__btn{
  align-self: center;
}
</style>
