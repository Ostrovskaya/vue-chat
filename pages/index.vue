<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8>
      <v-card min-width="400px">
        <Snackbar :message="message" :snackbar="snackbar"/>
        <v-card-title><h1>Nuxt чат</h1></v-card-title>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field v-model="name" :counter="16" :rules="nameRules" label="Ваше имя" required></v-text-field>

            <v-text-field v-model="room" :rules="roomRules" label="Введите комнату" required></v-text-field>

            <v-btn :disabled="!valid" color="primary" class="mr-4" @click="submit">Войти</v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import {mapMutations} from 'vuex'
import Snackbar from "../components/snackbar"
  export default {
    layout:"empty",
    head: {
      title: "Добро пожаловать в Nuxt чат"
    },
    components: {Snackbar},
    sockets:{
      connect() {
        console.log('socket connected')
      }
    },
    data: () => ({
      message: '',
      snackbar: false,
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Введите ия',
        v => (v && v.length <= 16) || 'Имя не должно превышать 16 символов',
      ],
      room: '',
      roomRules: [
        v => !!v || 'Введите комнату'
      ]
    }),
    methods: {
      ...mapMutations(["setUser"]),
      submit () {
        if(this.$refs.form.validate()){
          const user = {
            name: this.name,
            room: this.room
          };

          this.$socket.emit("userJoined", user, data => {
            if(typeof data == "string"){
              console.error(data);
            } else {
              user.id = data.userId;
              this.setUser(user);
              this.$router.push("/chat");
            }
          }); 
        }
      }
    },
    mounted() {
      const {message} = this.$route.query
      if(message == "leftChat"){
        this.message = "Вы покинули чат"
        this.snackbar = true;
      }
      if (message === 'noUser') {
        this.message = 'Введите данные';
        this.snackbar = true;
      }  
    }
  }
</script>
