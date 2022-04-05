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
  border: 1px solid rgb(224, 87, 224);
  background: rgb(233, 166, 233);
  border-radius: 8px;
  padding: 10px;
}
</style>
