<template>
  <div class="container">
<!--    ВХОД-->
    <my-dialog v-model:show="avtoVisible">
      <my-avto @sendAvto="avto" @closeForm="avtoVisible=false" @avtoVisible="avtoVisible=fasle"/>
    </my-dialog>
    <my-head
        @avtoVisible="avtoVisible = true"
        @exitUser="enterVisible=true"
        :enterVisible="enterVisible">
    </my-head>
    <div class="mainPage" v-if="seePortfolio">
      <div class="photo_basicInformation">
        <div class="photo">
          <img src="../public/img/leaf_rim.png">
        </div>
        <div class="basicInformation">
          <p class="title middle-title basicInformation-title">Основная информация</p>
          <div class="inf">
            <p><span>Возраст:</span> <span  style="color: black">{{basicInformation.age}}</span> </p>
            <p><span>Педагогический стаж:</span> <span  style="color: black"> {{basicInformation.experience}} </span></p>
            <p><span>Почта:</span> <span  style="color: black"> {{basicInformation.email}} </span></p>
            <p><span>Телефон:</span> <span style="color: black"> {{basicInformation.phone}} </span></p>
          </div>
          <my-button @click="getAwardsandEvents" class="green-button">Посмотреть портфолио</my-button>
        </div>
      </div>
      <div class="education">
        <p class="title middle-title title-block">Образование</p>
        <div class="inf-education">
          <p class="title-inf-education">Среднее специальное</p>
          <ul>
            <li>Нижегородский педагогический колледж</li>
            <li>Направление подготовки и (или) специальность — Дошкольное образование</li>
            <li>Квалификация по диплому — Руководитель физического воспитания</li>
          </ul>
          <p class="title-inf-education">Результаты аттестации</p>
          <p>Высшая квалификационная категория по должности инструктор по физической культуре (Образование)
            Дата аттестации — 31.01.2018</p>
          <p class="title-inf-education">Стаж</p>
          <ul>
            <li>Стаж работы — 23 лет 3 месяца 21 дней ( на 01.06.2023 )</li>
            <li>Педагогический стаж — 16 лет 8 месяцев 0 дней ( на 01.06.2023 )</li>
            <li>Стаж по специальности — 16 лет 8 месяцев 0 дней ( на 01.06.2023 )</li>
          </ul>
        </div>
      </div>
      <div class="reviews-block">
        <p class="title middle-title title-block">Отзывы</p>
        <my-button class="green-button" @click="reviewVisible = true">Написать отзыв</my-button>
        <div class="reviews">
          <my-reviews :reviews="reviews" :enterVisible="enterVisible" @deleteReview="deleteReview"></my-reviews>
        </div>
        <my-dialog v-model:show="reviewVisible">
          <add-review
              :review="review"
              @sendReview="sendReview"
              @reviewVisible="reviewVisible=false"
          />
        </my-dialog>
      </div>
    </div>
    <div class="portfolioPage" v-if="!this.seePortfolio">
      <my-button class="back-button" @click="seePortfolio = true">Назад</my-button>
      <my-dialog v-model:show="addAwardViisible">
        <add-award
            @addAwardViisible="addAwardViisible=false"
            @sendAward="sendAward"
        />
      </my-dialog>
      <div class="awards" style="position: relative">
        <add-button class="add-award" v-if="enterVisible==false" @click="addAwardViisible=true"/>
        <p class="title middle-title title-block" >Награды</p>
        <div class="inf-awards">
            <my-awards
                :awards="awards"
                @deleteAward="deleteAward"
                :enterVisible="enterVisible"
            ></my-awards>
        </div>
      </div>

      <my-dialog v-model:show="addEventVisible">
        <add-event
            @addEventVisible="addEventVisible=false"
            @sendEvent="sendEvent"
        />
      </my-dialog>

      <div class="events" style="position: relative">
          <add-button class="add-events" v-if="enterVisible==false" @click="addEventVisible=true"/>
          <p class="title middle-title title-block">Мероприятия</p>
        <div class="inf-events">
            <my-events :events="events"
                       class="events"
                        @deleteEvent="deleteEvent"
                       :enterVisible="enterVisible"
            >
            </my-events>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import myButton from "@/components/UI/myButton";
import myReviews from "@/components/myReviews";
import myHead from "@/components/myHead";
import myAwards from "@/components/myAwards";
import myEvents from "@/components/myEvents";
import myDialog from "@/components/myDialog";
import myAvto from "@/components/myAvto";
import addReview from "@/components/addReview";
import addButton from "@/components/UI/addButton";
import addAward from "@/components/addAward";
import addEvent from "@/components/addEvent";
export default {
  name: 'App',
  components: {myButton, myReviews, myHead, myAwards, myEvents, myDialog, myAvto, addReview, addButton, addAward, addEvent},
  data() {
    return {
      basicInformation: {
        age: '34 года',
        experience: '16 лет 8 месяцев 0 дней ( на 01.06.2023 )',
        email: 'mdoy_65@mail.ru',
        phone: '+79039462489',
      },
      reviews: [
        {id: 1, fio: 'Смирнова Наталья Ивановна',
          description: 'Замечательный воспитатель! Примите слова искренней благодарности за Ваш профессионализм, ' +
              'чуткое отношение, внимание и заботу к детям. Спасибо Вам за Ваше терпение, доброту, индивидуальный ' +
              'подход к каждому ребенку, за создание теплой и комфортной обстановки в группе.'},
      ],
      seePortfolio: true,
      awards: [
        {id: 1, src: 'https://nsportal.ru/sites/default/files/portfolio_photos/2017/08/23/svidetelstvo-2852291-213500.png'},
        {id: 2, src: 'https://nsportal.ru/sites/default/files/portfolio_photos/2017/09/13/004.jpg'},
        {id: 3, src: 'https://nsportal.ru/sites/default/files/portfolio_photos/2018/05/18/001_25.jpg'},
        {id: 4, src: 'https://nsportal.ru/sites/default/files/portfolio_photos/2018/10/03/tvu_001.jpg'},
        {id: 5, src: 'https://nsportal.ru/sites/default/files/portfolio_photos/2018/10/03/tv_001.jpg'},
      ],
      events: [
        {id: 1, src: 'https://www.maam.ru/upload/blogs/detsad-253470-1664732198.jpg',
          title: 'Квест-досуг для страших дошкольников "В поисках клада"',
          description: 'Цель: создать условия для развития интереса к самостоятельному командному решению поставленных задач через двигательную активность.' ,
        imgs: [{id: 1, src:'https://www.maam.ru/upload/blogs/detsad-253470-1664732198.jpg'},
          {id: 2, src:'https://www.maam.ru/upload/blogs/detsad-253470-1664732300.jpg'},
          {id: 3, src:'https://www.maam.ru/upload/blogs/detsad-253470-1664732082.jpg'}]},
        {id: 2, src: 'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2017/08/21/den_otkrytyh_dverey/20170322_081300.jpg?itok=MN0ZjTZp',
          title: 'День открытых дверей',
          description: 'Помни: рано или поздно твой сын последует твоему примеру, а не твоим советам.',
          imgs: [{id: 1, src:'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2017/08/21/den_otkrytyh_dverey/20170322_081300.jpg?itok=MN0ZjTZp'},
            {id:2, src:'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2017/08/21/den_otkrytyh_dverey/img_4936.jpg?itok=q747HLY3'},
            {id:3, src:'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2017/08/21/den_otkrytyh_dverey/img_4997.jpg?itok=dmPQa5P4'}]},
        {id: 3, src: 'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2018/05/18/futbol/88swohyfa0m.jpg?itok=NWO3z83v',
          title: 'Футбол',
          description: 'Футбол, как вид спорта для ребенка, имеет преимущества: ребенок станет физически развитым, причем очень быстро, укрепятся не только кости, но и мышечная ткань; тренировки включают разнообразные упражнения, работают все группы мышц, оказывается комплексная физическая нагрузка. Команда даст ребенку возможность почувствовать себя личностью, пусть и маленькой. ',
          imgs: [{id:1, src:'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2018/05/18/futbol/88swohyfa0m.jpg?itok=NWO3z83v'},
            {id:2, src:'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2018/05/18/futbol/img-20180420-wa0000.jpg?itok=3y4FjOBL'},
            {id:3, src:'https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2018/05/18/futbol/img-20180420-wa0010.jpg?itok=qMvLxUST'}]},
      ],
      sliderVisible: false,
      avtoVisible: false,
      user: {
        id: '1',
        login: 'mdoy_65@mail.ru',
        password: '~hGDHN|4',
      },
      enterVisible: true,
      reviewVisible: false,
      review: {
        id: '',
        fio: '',
        description: '',
      },
      editBasicInformationB: false,
      addAwardViisible: false,
      addEventVisible: false,
    }
  },
  methods: {
    openSlider(eventSlide) {
      this.eventSlide = eventSlide.imgs;
      this.sliderVisible = true;
      console.log(this.eventSlide);
    },
    avto(avto) {
      const value = localStorage[1];
      let userLocal = JSON.parse(value);
      console.log(value);
      console.log(avto);
      if (userLocal.login === avto.login && userLocal.password === avto.password) {
        this.enterVisible = false;
        alert('Вход успешно совершен!');
      } else {
        alert('Не правильно введенные данные')
      }
    },
    sendReview(review) {
      this.review = review;
      if ((/^[АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ][абвгдеёжзийклмнопрстуфхцчшщъыьэюя]{2,}$/.test(this.review.fio.split(' ')[0]))
        &&(/^[АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ][абвгдеёжзийклмнопрстуфхцчшщъыьэюя]{2,}$/.test(this.review.fio.split(' ')[1]))
      && (/^[АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ][абвгдеёжзийклмнопрстуфхцчшщъыьэюя]{2,}$/.test(this.review.fio.split(' ')[2]))) {
        if (review.description !== '') {
          this.reviews.push(this.review);
        } else {
          alert('Введите описание!')
        }
      } else {
        alert ('Введите корректные ФИО');
      }
      this.reviewVisible = false;
    },
    deleteReview(review) {
      this.reviews = this.reviews.filter(p=>p.id!==review.id);
    },
    sendAward(award) {
      if (award.src!=='') {
        this.awards.push(award);
        this.awards.id='award';
        localStorage.setItem(this.awards.id.toString(), JSON.stringify(this.awards));
      }
      this.addAwardViisible = false;
    },
    sendEvent(event) {
      if (event.src !== '' && event.title !== '' && event.description !== '' && event.imgs[1].src !== '' && event.imgs[2].src !== '') {
        event.imgs[0].src = event.src;
        this.events.push(event);
        this.events.id = 'events';
        localStorage.setItem(this.events.id.toString(), JSON.stringify(this.events));
      }
      this.addEventVisible = false;
    },
    getAwardsandEvents() {
      let v = localStorage.getItem('award');
      this.awards = JSON.parse(v);
      let ev = localStorage.getItem('events');
      this.events = JSON.parse(ev);
      this.seePortfolio = false;
    },
    deleteAward(award) {
      this.awards = this.awards.filter(p=>p.id!==award.id);
    },
    deleteEvent(event) {
      this.events = this.events.filter(p=>p.id!==event.id);
    }
  },
mounted() {
    localStorage.setItem(this.user.id.toString(), JSON.stringify(this.user));
    this.awards.id='award';
    localStorage.setItem(this.awards.id.toString(), JSON.stringify(this.awards));
    this.events.id = 'events';
    localStorage.setItem(this.events.id.toString(), JSON.stringify(this.events));
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500;1,600;1,700&family=Cormorant:wght@300;400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;300;400;500;600&display=swap');

#app {
  text-align: center;
}

* {
  box-sizing: border-box;
  font-family: 'Montserrat';
  font-size: 20px;
}

.container {
  padding: 0px 100px 50px;
}

.portfolioPage {
  position: relative;
}

.pink-button button {
  background-color: #FFAEDE;
  position: absolute;
  right: 0;
  top: 50px;
}

.pink-button button:hover {
  background-color: #ffc3e7;
  transition: background-color 0.3s;
}


.green-button button {
  background-color: #789E72;
  color: white;
  padding: 15px 30px;
}

.green-button button:hover {
  background-color: #96af93;
  transition: background-color 0.3s;
}

.back-button {
  padding: 10px;
  position: absolute;
  left: 0;
  top: -45px;
}

.title {
  font-family: 'Cormorant Garamond';
  font-weight: 700;
  line-height: 5px;
}

.middle-title {
  font-size: 32px;
  line-height: 5px;
}

.basicInformation-title::before {
  content: '';
  width: 25px;
  height: 30px;
  background: url("../public/img/icon _butterfly_.png") no-repeat center;
  display: inline-block;
  margin-right: 10px;
}

.title-block {
  margin-top: 50px;
}

.title-block::after {
  content: "";
  display: block;
  width: 450px;
  height: 0.5px;
  background-color: rgba(0, 0, 0, 0.5);
  margin-top: 15px;
  margin: 20px auto 35px;
}

.photo_basicInformation {
  display: flex;
  justify-content: center;
  gap: 100px;
  padding-top: 50px;
  text-align: left;
}

.photo {
  width: 350px;
  height: 350px;
  border-radius: 50%;
  background: url("https://nsportal.ru/sites/default/files/styles/media_gallery_large/public/gallery/2017/02/26/moi_uvlecheniya/sdc16435.jpg?itok=xUCoPY4b");
  position: relative;
}

.photo img {
  width: 400px;
  position: absolute;
  left: -35px;
  top: -15px;
}

.inf p {
  font-size: 20px;
  text-align: left;
  line-height: 15px;
}

.inf p span {
  color: #789E72;
}

.inf-education {
  background-color: #FFAEDE;
  width: 100%;
  z-index: -1;
  padding: 50px 100px;
  text-align: justify;
}

.title-inf-education {
  font-weight: 600;
}

.inf-events {
  background-color: #FFAEDE;
  padding: 50px;
}

.add-award button {
  top: -5px;
  left: 58%;
}

.add-events button {
  top: -5px;
  left: 58%;
}
</style>
