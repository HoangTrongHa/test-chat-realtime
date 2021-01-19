<template>
  <v-container>
      <v-form @submit.prevent="sendMessage">
          <v-text-field
            v-model="message"
          >
          </v-text-field>
          <v-btn
            type="submit"
          >send message</v-btn>
      </v-form>
  </v-container>
</template>

<script>
export default {
    data() {
        return {
            message: ''
        }
    },

    created() {
        Echo.channel('laravel_database_chatroom')
        .listen('.send.message', (data) => {
            console.log('socket listen ...')
        })
    },

    methods: {
        async sendMessage() {
            await this.$axios.get('http://localhost:8000/api/message').then(response => {
                console.log('ok')
            }).catch(err => {
                console.log(err)
            })
        }
    },
}
</script>

<style>

</style>