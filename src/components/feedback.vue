<template>

  <v-container class="d-flex justify-center flex-wrap rounded-lg" tile elevation="0">
    <h1 class="glitchTitle text-center mt-12 " id="formTitle" style="font-size: 70px; font-weight: bold" v-if="turnForm">
      Обратная связь</h1>
    <h1 class="glitchTitle text-center mt-12 " id="formTitle" style="font-size: 70px; font-weight: bold" v-else>
      Сообщение отправлено</h1>

    <div style="width: 80%" class="mx-auto my-12 py-12">

      <main class="box" v-if="turnForm">
        <v-form
            v-model="valid"
            validation
            id="feedback_form"
        >
          <v-text-field
              dark
              name="from_email"
              label="Email"
              type="email"
              v-model="from_email"
              :rules="emailRules"
          ></v-text-field>

          <v-textarea
              dark
              name="message"
              label="Сообщение"
              type="text"
              v-model="message"
              :rules="messageRules"
          ></v-textarea>

          <v-card-actions>
            <v-btn
                primary color="white"
                large
                block
                :disabled="!valid || loading"
                :loading="loading"
                @click="sendEmail"
                class="black--text"
            >Отправить
            </v-btn>
          </v-card-actions>
        </v-form>
      </main>
    </div>

  </v-container>

</template>

<script>
import emailjs from 'emailjs-com';

export default {
  name: "feedback",
  data() {
    return {
      from_email: '',
      message: '',
      valid: false,
      loading: false,
      turnForm: true,
      emailRules: [
        v => !!v || 'E-mail некоректный',
        v => /.+@.+\..+/.test(v) || 'E-mail должен быть коректным',
      ],
      messageRules: [
        v => !!v || 'Поле сообщения не должно быть пустым',
        v => v.length > 0 || 'Поле некоректно',
      ],
    }
  },
  methods: {
    sendEmail() {
      let form = document.querySelector('#feedback_form')

      try {
        emailjs.sendForm('service_govo1bo', 'template_fhrbhue', form, 'user_a2H47lOOmuFo3FydFf1oT', {
          email: this.from_email,
          message: this.message,
        })
        this.from_email = ''
        this.message = ''
        this.turnForm = false
        setTimeout(()=>{
          this.turnForm = true
        }, 2000)
      } catch (error) {
        console.log({error})
      } // Reset form field this.name = '' this.email = '' this.message = '' },
    },
  }
}
</script>

<style lang="scss" scoped>
@font-face {
  font-family: 'Pixel Font';
  src: url("../assets/fonts/pixelFont.ttf");
  //src: url("../assets/fonts/pixelFont.ttf");
  font-style: normal;
  font-weight: normal;
}


.w-100 {
  width: 100%;
}

#formTitle {
  font-family: "Pixel Font";
  color: white;
}

</style>