<template>
  <div class="dialog" v-if="show" @click="hideDialog">
    <div class="dialogContent" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    hideDialog() {
      this.$emit('update:show', false);
    }
  }
}
</script>

<style scoped>
.dialog {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  z-index: 100;
}
.dialogContent {
  margin: auto;
  position: relative;
  background-repeat: no-repeat;
  background-size: contain;
  border-radius: 10px;
  padding: 20px;
  min-width: 300px;
}

</style>