<template>
  <div class="reviews" v-if="reviews.length>0">
    <my-review v-for="review in reviews"
               :review="review"
               :key="review.id"
               :enterVisible="enterVisible"
               @deleteReview="$emit('deleteReview', review)"
    >
    </my-review>
  </div>
  <div v-else>Отзывов нет</div>
</template>

<script>
import myReview from "@/components/myReview";
export default {
  components: {myReview},
  props: {
    reviews: {
      type: Array,
      required: true,
    },
    enterVisible: {
      type: Boolean,
      default: false,
    },
  }
}
</script>

<style scoped>
  .reviews {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 70px;
    margin-top: 40px;
  }
</style>
