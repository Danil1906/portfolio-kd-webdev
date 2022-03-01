<template>
  <v-dialog v-model="modal" id="modalInExamples" max-width="70%">
    <template v-slot:activator="{ on }">
      <v-col
          tag="button"
          v-on="on"
          v-for="ex in examples"
          :key="ex.title"
          class="col-xs-12 col-md-4 d-flex justify-center align-center exampleImg"

      >

        <div
            @click="currentExam=ex.title"

        >


          <svg width="350" id="svgFolder"  enable-background="new 0 0 150 150" viewBox="0 0 64 64">
            <path fill="#62c5e8" d="M61.9,57.4H4.3c-1.1,0-2.1-0.9-2.1-2.1V13.4c0-1.1,0.9-2.1,2.1-2.1H33c0.8,0,1.5-0.4,1.8-1.1l1.7-3.4
		c0.4-0.7,1.1-1.1,1.8-1.1h23.5c1.1,0,2.1,0.9,2.1,2.1v47.5C64,56.4,63.1,57.4,61.9,57.4z"/>
            <path fill="#49a8c3" d="M61,58.3H4.3c-1.1,0-2.1-0.9-2.1-2.1V14.3c0-1.1,0.9-2.1,2.1-2.1H33c0.8,0,1.5-0.4,1.8-1.1l1.7-3.4
		c0.4-0.7,1.1-1.1,1.8-1.1h23.5c1.1,0,2.1,0.9,2.1,2.1v46.6C64,56.9,62.7,58.3,61,58.3z"/>
            <path fill="#70ceea" d="M0,18.6l0,35.8c0,1.7,1.3,3,3,3h58c1.7,0,3-1.3,3-3v-31c0-1.7-1.3-3-3-3H31.8c-0.8,0-1.6-0.3-2.1-0.9l-3-3
		c-0.6-0.6-1.3-0.9-2.1-0.9H3C1.3,15.6,0,17,0,18.6z"/>
            <path fill="#62c5e8" d="M0,19.5l0,35.8c0,1.7,1.3,3,3,3h58c1.7,0,3-1.3,3-3v-31c0-1.7-1.3-3-3-3H31.8c-0.8,0-1.6-0.3-2.1-0.9l-3-3
		c-0.6-0.6-1.3-0.9-2.1-0.9H3C1.3,16.5,0,17.9,0,19.5z"/>
            <image :href="getImgUrl(ex.image[0])" x="2" y="11" height="60px" width="60px" />
          </svg>

        </div>
      </v-col>
    </template>

    <template >
      <div
          v-for="ex in examples"
          :key="ex.title">

        <v-card
            id="examplesModalViews"
            class="mx-auto"
            max-width="100%"
            max-height="95%"
            v-if="currentExam === ex.title "

        >
          <v-carousel
              height="auto"
              :continuous="false"
              :cycle="cycle"
              hide-delimiter-background
              delimiter-icon="mdi-minus"

          >
            <v-carousel-item
                v-for="image in ex.image"
                :key="image"
                :src="getImgUrl(image)"
            >

            </v-carousel-item>
          </v-carousel>

          <v-card-text class="text--primary">

            <v-list>
              <v-list-group
              >
                <template v-slot:activator>
                  <v-list-item-content>
                    <v-list-item-title v-text="'Используемые в проекте инструменты'"
                                       class="light-blue--text"></v-list-item-title>
                  </v-list-item-content>
                </template>

                <v-list-item
                    v-for="item in filterTextSplit(ex.technologies)"
                    :key="item"
                >
                  <v-list-item-content>
                    <v-list-item-title v-text="item"></v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list-group>
            </v-list>

            <p>{{ ex.description }}</p>

          </v-card-text>
        </v-card>
      </div>
    </template>
  </v-dialog>
</template>

<script>
import $ from "jquery";

export default {
  name: "modalView",
  data() {
    return {
      modal: false,
      examples: [
        {
          "image": ["ChasDet_webp/Chas3.webp", "ChasDet_webp/Chas1.webp", "ChasDet_webp/Chas2.webp"],
          "title": "chasDet",
          "moreImage": ["ChasDet_webp/Chas3.webp", "ChasDet_webp/Chas1.webp", "ChasDet_webp/Chas2.webp"],
          "description": "Полноценный интернет магазин." +
              "По ТЗ требовалось создать магазин с неограниченной вложенностью категорий, максимально простой во внешнем виде" +
              " в соответствии целевой аудитории, в цветах логотипа и не насыщенный динамикой." +
              "Система регистрации и авторизации, разделение пользователей на оптовых и рознечных." +
              "Система восстановления пароля." +
              "Обратная связь." +
              "Корзина со своей спецификой из за особенности бизнесслогики заказчика." +
              "Система оформления заказа, сдек, почта рф запакованная в  api яндекс карт, так же не подходили готовые решения" +
              "виджетов из за специфики бизнеслогики." +
              "Множество решений в административной панели для гибкого управления сайтом." +
              "Адаптация под устройства." +
              "Оптимизация путем сокращения запросов к БД, исползования SVG и WebP форматов. Минимизации кода." +
              "Система поиска по товарам",
          "technologies": "HTML." +
              "Java Script." +
              "jQuery." +
              "CSS." +
              "Sass." +
              "Bootstrap." +
              "Django." +
              "Gulp." +
              "Python." +
              "npm." +
              "Git." +
              "Postgre SQL." +
              "Yandex Map Api." +
              "CDEK Api." +
              "Pochta Rossii Api."
        },
        {
          "image": ["7_webP/TechStore.webp"], "title": "TechStore",
          "moreImage": false,
          "description": "Проект с использованием только компонентов Vue JS с Firebase сервисами (Realtime Database, Authentication, Storage)",
          "technologies": "Vue JS." +
              "Vuetify." +
              "Firebase." +
              "HTML." +
              "CSS." +
              "Java Script."
        },
        {
          "image": ["6_webP/Disign.webp", "6_webP/Disign2.webp", "6_webP/Disign3.webp"], "title": "Design",
          "moreImage": ["6_webP/Disign.webp", "6_webP/Disign2.webp", "6_webP/Disign3.webp"],
          "description": "Переснос готового макета и создание функционала для него.",
          "technologies": "Python." +
              "Django." +
              "CSS." +
              "Java Script." +
              "jQuery." +
              "Git." +
              "SQLlite." +
              "HTML." +
              "Sass." +
              "Bootstrap."
        },
        {
          "image": ["5_webP/OneStr1.webp", "5_webP/OneStr2.webp", "5_webP/OneStr3.webp"], "title": "OneStr",
          "moreImage": ["5_webP/OneStr1.webp", "5_webP/OneStr2.webp", "5_webP/OneStr3.webp"],
          "description": "Одностраничкик чистом CSS, HTML, css анимация, паралакс",
          "technologies": "HTML." +
              "CSS."
        },
        {
          "image": ["4_webP/ShopMe1.webp", "4_webP/ShopMe2.webp", "4_webP/ShopMe3.webp", "4_webP/ShopMe4.webp"],
          "title": "ShopMe",
          "moreImage": ["4_webP/ShopMe1.webp", "4_webP/ShopMe2.webp", "4_webP/ShopMe3.webp", "4_webP/ShopMe4.webp"],
          "description": "Онлайн магазин курсов. " +
              "Система регистрации/авторизации." +
              "MySQL." +
              "Система платежей.",
          "technologies": "Django." +
              "Python." +
              "Java Script." +
              "Git." +
              "jQuery." +
              "CSS." +
              "Sass." +
              "HTML." +
              "npm." +
              "Bootstrap."
        },
        {
          "image": ["3_webP/JUSTBLOG1.webp", "3_webP/JUSTBLOG2.webp", "3_webP/JUSTBLOG3.webp", "3_webP/JUSTBLOG4.webp"],
          "title": "JustBlog",
          "moreImage": ["3_webP/JUSTBLOG1.webp", "3_webP/JUSTBLOG2.webp", "3_webP/JUSTBLOG3.webp", "3_webP/JUSTBLOG4.webp",],
          "description": "Работа с БД." +
              "Система авторизации/регистрации" +
              "Тесная работа с БД со странички 'добавление/удаление/редактирование новостей. Редактирование информации профиля.'",
          "technologies": "Django." +
              "Python." +
              "Java Script." +
              "Git." +
              "jQuery." +
              "CSS." +
              "Sass." +
              "HTML." +
              "npm." +
              "Bootstrap."
        }
      ],
      currentExam: ''
    }
  },
  methods: {
    getImgUrl(pic) {
      return require('@/assets/sprite/image/' + pic);
    },

    filterTextSplit(str) {
      return str.split('.')
    }
  },
  mounted() {
    let exImg = document.querySelectorAll('.exampleImg')
    exImg.forEach((el) => {
      $(el).on('mouseover', () => {
        $(el).addClass('exampleImgAnimation')
      })

      $(el).on('mouseleave', () => {
        $(el).removeClass('exampleImgAnimation')
      })
    })
  }
}
</script>

<style lang="scss" scoped>
@font-face {
  font-family: 'Pixel Font';
  src: url("../assets/fonts/pixelFont.ttf");
  font-style: normal;
  font-weight: normal;
}


.exampleImgAnimation {
  animation: oldStyleSelect linear infinite 2s;

  @keyframes oldStyleSelect {
    100% {
      opacity: 1;

    }

    67% {
      opacity: 0.5;
    }

    34% {
      opacity: 0;
    }

    0% {
      opacity: 0.5;
    }
  }
}

#examplesModalViews {
  font-family: "Pixel Font";
}

.imgBorderColor {
  border: 1px solid black;
}


</style>