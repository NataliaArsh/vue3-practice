<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
export default {
  name: 'my-button'
}
</script>


<style scoped>
.btn {
  height: 40px;
  min-width: 100px;
  border: 1px solid rgb(219, 116, 219);
  background: rgb(246, 222, 246);
  border-radius: 8px;
  padding: 10px;
}
</style>
