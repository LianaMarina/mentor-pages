<template>
  <div>
    <form class="avto-form" action="" @submit.prevent>
      <close-button @click="$emit('addAwardViisible', false)">х</close-button>
      <h3 class="title-form">Добавление награды</h3>
      <input type="text" v-model="award.src" placeholder="Ссылка на фото">
      <button class="form-button" @click="sendAward">Добавить</button>
    </form>
  </div>
</template>

<script>
import closeButton from "@/components/UI/closeButton";
export default {
  components: {closeButton},
  data() {
    return {
      award: {
        id: '',
        src: '',
      }
    }
  },
  methods: {
    sendAward() {
      this.award.id = Date.now();
      this.$emit('sendAward', this.award);
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