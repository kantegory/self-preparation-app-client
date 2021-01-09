<template>
  <main class="wrapper">
    <v-col cols="6" class="mx-auto">

      <v-card
        v-for="ticket in tickets"
        :key="ticket.id"
        color="primary"
        dark
        class="my-2"
      >
        <v-card-title>
          Вопрос №{{ ticket.id }}
        </v-card-title>
        <v-card-subtitle>
          <strong>Текст вопроса</strong>: {{ ticket.questions }}
        </v-card-subtitle>
        <v-card-text>
          <v-switch
            v-model="ticket.isAnswerShowed"
            inset
            label="Показывать ответ"
          ></v-switch>
        </v-card-text>
        <v-card-text v-if="ticket.isAnswerShowed">
          <strong>Текст ответа</strong>: {{ ticket.answers }}
        </v-card-text>
      </v-card>

    </v-col>
  </main>
</template>

<script>
export default {
  name: 'Tickets',

  data: () => ({
    tickets: []
  }),

  methods: {
    async loadAllTickets () {
      try {
        const response = await this.axios({
          method: 'GET',
          url: `http://localhost:8000/tickets/Algebra?user_id=${localStorage.getItem('userId')}`
        })

        if (response.status !== 200) {
          throw new Error(response.error)
        }

        this.tickets = response.data.map((ticket) => {
          ticket.isAnswerShowed = false

          return ticket
        })
      } catch (e) {
        console.error('AN API ERROR', e)
      }
    }
  },

  mounted () {
    this.loadAllTickets()
  }
}
</script>
