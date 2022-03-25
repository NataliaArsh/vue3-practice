<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
export default {
}
</script>


<style scoped>
.btn {
  height: 30px;
  width: 100px;
  border: 1px solid rgb(224, 87, 224);
  background: rgb(233, 166, 233);
}
</style>
