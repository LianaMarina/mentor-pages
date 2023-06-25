<template>
  <div class="event" style="position: relative">
    <delete-button class="del-button" @click="$emit('deleteEvent', event)" v-if="enterVisible==false">Удалить</delete-button>
    <img :src="event.src" alt="event-img" @click="sliderVisible = true">
    <div class="event-text">
      <p class="event-title">{{event.title}}</p>
      <p class="event-description">{{event.description}}</p>
      <my-dialog v-model:show="sliderVisible">
        <my-awards class="eventSlider" :awards="event.imgs"></my-awards>
      </my-dialog>
    </div>
  </div>
</template>

<script>
import myAwards from "@/components/myAwards";
import myDialog from "@/components/myDialog";
import deleteButton from "@/components/UI/deleteButton";

export default {
  components: {myAwards, myDialog, deleteButton},
  props: {
    event: {
      type: Object,
      required: true,
    },
    enterVisible: {
      type: Boolean,
      required: true,
      default: true,
    },
  },
  data() {
    return {
      sliderVisible: false,
    }
  }
}
</script>

<style scoped>
.event {
  background: #F5F5F5;
  display: flex;
  margin: 30px 50px;
  border-radius: 15px;
}

.event img {
  width: 320px;
  height: auto;
  object-fit: cover;
  border-radius: 15px 0 0 15px;
  cursor: pointer;
  transition: .5s;
}

.event img:hover {
  width: 340px;
}

.event-text {
  padding-left: 50px;
  padding-right: 50px;
  text-align: justify;
}

.event-title {
  color: #789E72;
  font-size: 20px;
  font-weight: 500;
  line-height: 25px;
}

.event-description {
  font-size: 18px;
}

.del-button {
  top: 10px;
  right: 20px;
}

.delete-button {
  display: none;
}
</style>