<template>
  <h3>Создание поста</h3>
  <form class="form" @submit.prevent>
    <my-input
      v-focus
      placeholder="Введите название"
      v-model="post.title"
    >  
    </my-input> 
    <my-input
      placeholder="Введите описание"
      v-model="post.body"
    >    
    </my-input> 
    <my-button
      @click="addPost"
      class="btn-form"
    >Добавить
    </my-button>
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

.btn-form {
  align-self: end;
}
</style>
