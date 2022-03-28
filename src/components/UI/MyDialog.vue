<template>
    <div class="dialog" v-if="show" @click.stop="hideDialoge">
        <div @click.stop class="dialog__content">
            <slot></slot>
        </div>       
    </div>
</template>

<script>
export default {
  name: 'my-dialog',
  props: {
    show: {
        type: Boolean,
        default: false
    },
  },
  methods: {
      hideDialoge() {
          this.$emit('update:show', false)
      }
  }
}
</script>


<style scoped>
.dialog {
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: rgb(0, 0, 0, 0.5);
    position: fixed;
    display: flex;
}
.dialog__content {
    margin: auto;
    padding: 15px;
    background: white;
    border-radius: 12px;
    min-height: 180px;
    min-width: 350px;
}
</style>
