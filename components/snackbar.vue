<template>
  <div class="text-center ma-2">
    <v-snackbar v-model="snackbar" :timeout="6000" top>
      {{ message }}
      <v-btn color="pink" text @click="snackbar = false">
        Закрыть
      </v-btn>
    </v-snackbar>
  </div>
</template>

<script>
  export default {
    data: () => ({
      
    }),
    props: {
        message: String,
        snackbar: false
    }
  }
</script>