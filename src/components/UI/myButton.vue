<template>
  <div>
    <button>
      <slot></slot>
    </button>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
  button {
    text-transform: uppercase;
    padding: 10px 30px 7px;
    border-radius: 10px;
    border: solid 1px black;
    font-size: 18px;
    cursor: pointer;
  }
</style>