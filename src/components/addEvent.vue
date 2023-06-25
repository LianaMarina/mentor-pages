<template>
  <div>
    <form class="avto-form" action="" @submit.prevent>
      <close-button @click="$emit('addEventVisible', false)">х</close-button>
      <h3 class="title-form">Добавление мероприятия</h3>
        <input type="text" v-model="event.src" placeholder="Ссылка на фото">
        <input type="text" v-model="event.imgs[1].src" placeholder="Ссылка на фото">
        <input type="text" v-model="event.imgs[2].src" placeholder="Ссылка на фото">
      <input type="text" v-model="event.title" placeholder="Название мероприятия">
      <textarea type="text" v-model="event.description" placeholder="Описание мероприятия"></textarea>
      <button class="form-button" @click="sendEvent">Добавить</button>
    </form>
  </div>
</template>

<script>
import closeButton from "@/components/UI/closeButton";
export default {
  components: {closeButton},
  data() {
    return {
      event: {
        id: '',
        src: '',
        title: '',
        description: '',
        imgs: [{id: 1, src: ''}, {id: 2, src: ''}, {id: 3, src: ''}],
      }
    }
  },
  methods: {
    sendEvent() {
      this.event.id = Date.now();
      this.$emit('sendEvent', this.event);
    },
  }
}
</script>

<style scoped>
.avto-form {
  background: #789E72;
  padding: 25px 80px 30px;
  border-radius: 15px;
  border: 1px solid black;
  overflow-y:scroll;
  height: 690px;
  position:relative;
}

.title-form {
  text-transform: uppercase;
  color: #FFFF;
  font-size: 32px;
}

.title-form:after {
  content: "";
  display: block;
  width: 450px;
  height: 1px;
  background-color: rgb(255, 255, 255);
  margin: 20px auto 35px;
}

input, textarea {
  display: block;
  min-width: 660px;
  padding: 10px 30px;
  border-radius: 15px;
  background: #F5F5F5;
  margin-bottom: 15px;
  border: 1px solid black;
  font-size: 18px;
}

input::placeholder, textarea::placeholder {
  font-size: 15px;
}

textarea {
  min-height: 280px;
}

button.form-button{
  background-color: #FFAEDE;
  font-weight: 500;
  margin-top: 30px;
  text-transform: uppercase;
  padding: 10px 30px 7px;
  border-radius: 10px;
  border: solid 1px black;
  font-size: 18px;
  cursor: pointer;
}

button.form-button:hover {
  background-color: #ffc3e7;
  transition: background-color 0.3s;
}

</style>