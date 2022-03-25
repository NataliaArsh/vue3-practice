<template>
  <form class="form" @submit.prevent>
    <input 
      type="text" 
      placeholder="Введите название"
      v-model="post.title"
    >
    <input 
      type="text" 
      placeholder="Введите описание"
      v-model="post.body"
    >
    <my-button
      @click="addPost"
      class="btn-form"
    >Добавить
    </my-button>
  </form>
</template>

<script>
import MyButton from './UI/MyButton.vue';
export default {
  components: { MyButton },
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    addPost() {
      this.post.id = Date.now();
      this.$emit('add', this.post);
      this.post = {
        title: '',
        body: '',
      };
    }
  }
}
</script>


<style scoped>
form {
  display: flex;
  flex-direction: column;
}

input {
  display: inline-block;
  width: 100%;
  height: 35px;
  border: 2px solid rgb(224, 87, 224);
  margin-bottom: 10px;
  padding-left: 5px;
}

.btn-form {
  align-self: end;
}
</style>
