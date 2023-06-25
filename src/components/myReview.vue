<template>
  <div class="review">
    <delete-button class="del-button" v-if="enterVisible==false" @click="$emit('deleteReview', review)">Удалить</delete-button>
    <p class="review-fio">{{review.fio}}</p>
    <p class="review-description">{{review.description}}</p>
  </div>
</template>

<script>
import deleteButton from "@/components/UI/deleteButton";
  export default {
    components: {deleteButton},
    props: {
      review: {
        type: Object,
        required: true,
      },
      enterVisible: {
        type: Boolean,
        default: true,
      },
    }
  }
</script>

<style scoped>
  .review {
    background-color: #F5F5F5;
    width: 550px;
    padding: 30px 40px;
    border-radius: 15px;
    box-shadow: 3px 6px 10px 5px rgba(0, 0, 0, 0.2);
    position: relative;
  }

  .review-fio {
    color: #789E72;
    font-size: 24px;
    line-height: 25px;
    font-weight: 500;
  }

  .review-description {
    font-size: 18px;
    position: relative;
  }

  .review-description::before {
    content: "\201c";
    font-size: 64px;
    color: #FFAEDE;
    position: absolute;
    top: -10px;
    left: -15px;
  }

  .review-description::after {
    content: "\201c";
    font-size: 64px;
    color: #FFAEDE;
    position: absolute;
    right: -15px;
  }

  .del-button button {
    top: 10px;
    right: 25px;
  }
</style>