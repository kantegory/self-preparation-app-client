<template>
  <auth-base-layout>
    <sign-up-form />
  </auth-base-layout>
</template>
<script>
import SignUpForm from '@/components/auth/SignUpForm'
import AuthBaseLayout from '@/layouts/auth/BaseLayout'

export default {
  name: 'SignUp',

  components: {
    SignUpForm,
    AuthBaseLayout
  }
}
</script>
