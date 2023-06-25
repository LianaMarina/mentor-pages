<template>
  <div class="slider-buttons" v-if="awards.length>0">
    <button class="arrow-back" @click="backSlide"></button>
    <div class="wrapper">
      <div class="slider" :style="{ 'margin-left': '-' + (100*currentSlideIndex) + '%' }">
        <my-award
            v-for="award in awards"
            :key="award.id"
            :award="award"
            @deleteAward="$emit('deleteAward', award)"
            :enterVisible="enterVisible"
        />
      </div>
    </div>
    <button class="arrow-forward" @click="forwardSlide"></button>
  </div>
  <div v-else>Наград нет</div>
</template>

<script>
import myAward from "@/components/myAward";
export default {
  components: {myAward},
  props: {
    awards: {
      type: Array,
      required: true,
    },
    enterVisible: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      currentSlideIndex: 0,
    }
  },
  methods: {
    backSlide() {
      if (this.currentSlideIndex > 0) {
        this.currentSlideIndex--;
      }
    },
    forwardSlide() {
      if (this.currentSlideIndex >= this.awards.length-1) {
        this.currentSlideIndex = 0;
      } else {
        this.currentSlideIndex++;
      }
    }
  }
}
</script>

<style scoped>
.slider-buttons {
  display: flex;
  align-items: center;
  position: relative;
}

.slider {
  display: flex;
  transition: all ease .5s;
}

button {
  width: 50px;
  height: 50px;
  background-repeat: no-repeat;
  background-size: contain;
  border: none;
  background: none;
  cursor: pointer;
  margin: 10px;
}

.arrow-back {
  background-image: url("../../public/img/arrow-back.png");
}

.arrow-forward {
  background-image: url("../../public/img/arrow-forward.png");
}

.wrapper {
  max-width: 500px;
  overflow: hidden;
  margin: 0 auto;
}
</style>