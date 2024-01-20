<template>
  <div class="flex" style="display: flex">
    <form @submit.prevent="onsubmit">
      <va-input
        v-model="username"
        class="mb-3"
        placeholder="用户名"
        :error="!!usernameErrors.length"
        :error-messages="usernameErrors"
      />

      <va-input
        v-model="password"
        class="mb-3"
        type="password"
        placeholder="密码"
        :error="!!passwordErrors.length"
        :error-messages="passwordErrors"
      />

      <div class="auth-layout__options d-flex align-center justify-space-between">
        <va-checkbox v-model="keepLoggedIn" class="mb-0" :label="t('auth.keep_logged_in')" />
        <router-link class="ml-1 va-link" :to="{ name: 'recover-password' }">{{
          t('auth.recover_password')
        }}</router-link>
      </div>

      <div class="d-flex justify-center mt-3">
        <va-button class="my-0" style="width: 200px" @click="onsubmit">{{ t('auth.login') }}</va-button>
      </div>
    </form>
    <div style="display: flex; flex-direction: column; align-items: center; margin-left: 40px">
      <div>扫码登录</div>
      <img class="qrcode" src="/qrcode.png" alt="" />
    </div>
  </div>
</template>

<script setup lang="ts">
  import { computed, ref } from 'vue'
  import { useRouter } from 'vue-router'
  import { useI18n } from 'vue-i18n'
  import axios from 'axios'
  const { t } = useI18n()

  const username = ref('')
  const password = ref('')
  const keepLoggedIn = ref(false)
  const usernameErrors = ref<string[]>([])
  const passwordErrors = ref<string[]>([])
  const router = useRouter()

  const formReady = computed(() => !usernameErrors.value.length && !passwordErrors.value.length)

  function onsubmit() {
    usernameErrors.value = username.value ? [] : ['请输入账号']
    passwordErrors.value = password.value ? [] : ['请输入密码']
    if (formReady.value) {
      axios.get('/users.json').then((response) => {
        const users = response.data
        const user = users.find((user) => user.username == username.value)
        if (user) {
          if (user.password == password.value) {
            return router.push({ name: 'main' })
          } else {
            passwordErrors.value = ['密码错误']
          }
        } else {
          usernameErrors.value = ['无此账号']
        }
      })
    }
  }
</script>

<style>
  .qrcode {
    width: 150px;
  }
</style>
