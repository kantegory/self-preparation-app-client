<template>
  <v-form
    @submit.prevent="register"
    ref="form"
  >
    <v-text-field
      label="Логин"
      v-model="form.login"
    />
    <v-text-field
      label="Имя"
      v-model="form.firstname"
    />
    <v-text-field
      label="Фамилия"
      v-model="form.lastname"
    />
    <v-text-field
      label="Email"
      type="email"
      v-model="form.email"
    />
    <v-text-field
      label="Пароль"
      type="password"
      v-model="form.password"
    />

    <v-btn
      type="submit"
      color="primary"
      dark
    >
      Регистрация
    </v-btn>
  </v-form>
</template>

<script>
export default {
  name: 'SignUpForm',

  data: () => ({
    form: {
      login: '',
      firstname: '',
      lastname: '',
      email: '',
      password: ''
    }
  }),

  methods: {
    async register () {
      console.log('FORM', this.form)

      try {
        const response = await this.axios({
          method: 'POST',
          url: 'http://localhost:8000/users/',
          data: this.form
        })

        if (response.status !== 201 && response.status !== 200) {
          throw new Error(response.error)
        }

        // очищаем форму
        this.$refs.form.reset()

        // сохраняем данные по юзеру
        const userId = response.data.id
        localStorage.setItem('userId', userId)

        // редиректим пользователя на авторизацию
        this.$router.push('/tickets')
      } catch (e) {
        console.error('AN API ERROR', e)
      }
    }
  }
}
</script>
