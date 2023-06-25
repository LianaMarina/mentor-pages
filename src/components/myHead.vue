<template>
  <div>
    <div class="fio_button">
      <h3 class="title fio">{{fio}}</h3>
      <my-button v-if="enterVisible" class="pink-button" @click="$emit('avtoVisible', true)">Войти</my-button>
      <my-button v-if="enterVisible==false" class="pink-button" @click="$emit('exitUser', true)">Выйти</my-button>
    </div>
    <p class="mentor text">инструктор по физической культуре</p>
  </div>
</template>

<script>
import myButton from "@/components/UI/myButton";
export default {
  components: {myButton},
  props:{
    enterVisible: {
      type: Boolean,
      default: true,
    }
  },
data() {
  return{
    fio: 'Ушакова Татьяна Владимировна',
  }
},
}
</script>

<style scoped>
.fio_button {
  display: flex;
  justify-content: center;
  position: relative;
}


.fio {
  font-size: 40px;
  line-height: normal;
}

.mentor, button, .inf p span {
  font-weight: 500;
}

p.mentor::after {
  content: "";
  display: block;
  width: 100%;
  height: 1px;
  background-color: rgba(0, 0, 0, 0.5);
  margin-top: 15px;
}

.pink-button button {
  position: absolute;
  right: 0;
  top: 50px;
}

</style>