<template>
  <form @submit.prevent="onsubmit()">
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
      <va-checkbox
        v-model="agreedToTerms"
        class="mb-0"
        :error="!!agreedToTermsErrors.length"
        :error-messages="agreedToTermsErrors"
      >
        <template #label>
          <span class="ml-2">
            {{ t('auth.agree') }}
            <span class="va-link">{{ t('auth.termsOfUse') }}</span>
          </span>
        </template>
      </va-checkbox>
      <router-link class="ml-1 va-link" :to="{ name: 'recover-password' }">
        {{ t('auth.recover_password') }}
      </router-link>
    </div>

    <div class="d-flex justify-center mt-3">
      <va-button class="my-0" style="width: 200px" @click="onsubmit">{{ t('auth.sign_up') }}</va-button>
    </div>
  </form>
</template>

<script setup lang="ts">
  import { ref, computed } from 'vue'
  import { useRouter } from 'vue-router'
  import { useI18n } from 'vue-i18n'
  import axios from 'axios'
  const { t } = useI18n()

  const username = ref('')
  const password = ref('')
  const agreedToTerms = ref(false)
  const usernameErrors = ref<string[]>([])
  const passwordErrors = ref<string[]>([])
  const agreedToTermsErrors = ref<string[]>([])
  const router = useRouter()

  const formReady = computed(() => {
    return !(usernameErrors.value.length || passwordErrors.value.length || agreedToTermsErrors.value.length)
  })

  function onsubmit() {
    usernameErrors.value = username.value ? [] : ['请输入用户名']
    passwordErrors.value = password.value ? [] : ['请输入密码']
    agreedToTermsErrors.value = agreedToTerms.value ? [] : ['您必须同意使用条款才能继续']

    if (formReady.value) {
      axios.get('/users.json').then((response) => {
        const users = response.data
        if (users.find((user: any) => user.username == username.value)) {
          usernameErrors.value = ['用户已存在']
        } else {
          users.push({ username: username.value, password: password.value })
          router.push({ name: 'main' })
        }
      })
    }
  }
</script>
