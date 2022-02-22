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
    <button
      @click="addPost"
    >Добавить</button>
  </form>
</template>

<script>
export default {
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

button {
  align-self: end;
  height: 30px;
  width: 100px;
  border: 1px solid rgb(224, 87, 224);
  background: rgb(233, 166, 233);
}
</style>
