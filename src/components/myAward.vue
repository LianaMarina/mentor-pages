<template>
  <div class="slider">
    <div class="sliderImg" style="position: relative">
      <img v-bind:src="award.src" alt="img-slider">
      <delete-button v-if="enterVisible==false" class="delete-award"
                     @click="$emit('deleteAward', award)" style="bottom: 0; right: 0"/>
    </div>
  </div>
</template>

<script>
import deleteButton from "@/components/UI/deleteButton";
export default {
  components: {deleteButton},
  props: {
    award: {
      type: Object,
      required: true,
    },
    enterVisible: {
      type: Boolean,
      required: true,
    }
  }
}
</script>

<style>
.sliderImg {
  width: 500px;
  height: auto;
}

.sliderImg img {
  width: 100%;
  height: auto;
  position: center;
}
</style>