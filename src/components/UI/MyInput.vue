<template>
    <input type="text" class="input" v-model="modelValue" @input="updateInput">
</template>

<script>
export default {
  name: 'my-input',
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>


<style scoped>
.input {
  display: inline-block;
  width: 100%;
  height: 35px;
  border: 2px solid rgb(224, 87, 224);
  margin-bottom: 10px;
  padding-left: 5px;
}

</style>
