<template>
  <div class="auth-layout row">
    <img class="bgpic1" src="/bgpic1.png" />
    <img class="bgpic2" src="/bgpic2.png" />
    <img class="bgpic4" src="/bgpic4.png" />
    <div class="flex xs12 pa-3 justify-center">
      <div class="py-1 justify-center d-flex">
        <div style="text-align: center; color: #fff">
          <h1 class="titleen">Bus Driver Safety Digital Portrait System</h1>
          <h1 class="titlecn">公交驾驶员行车安全数字画像系统</h1>
        </div>
      </div>
    </div>

    <video id="myVideo" autoplay muted loop>
      <source src="/bg.mp4" type="video/mp4" />
      Your browser does not support HTML5 video.
    </video>

    <div class="flex xs12 pa-3">
      <div class="d-flex justify-center">
        <va-card class="auth-layout__card">
          <va-card-content>
            <va-tabs v-model="tabIndex" center>
              <template #tabs>
                <va-tab name="login">{{ t('auth.login') }}</va-tab>
                <va-tab name="signup">{{ t('auth.createNewAccount') }}</va-tab>
              </template>
            </va-tabs>

            <va-separator />

            <div class="pa-3">
              <router-view />
            </div>
          </va-card-content>
        </va-card>
      </div>
    </div>
  </div>
</template>

<script>
  import { useI18n } from 'vue-i18n'

  export default {
    name: 'AuthLayout',
    setup() {
      const { t } = useI18n()
      return { t }
    },
    data() {
      return {
        selectedTabIndex: 0,
      }
    },
    computed: {
      tabIndex: {
        set(tabName) {
          this.$router.push({ name: tabName })
        },
        get() {
          return this.$route.name
        },
      },
    },
  }
</script>

<style lang="scss" scoped>
  .auth-layout {
    min-height: 100vh;
    // background-image: linear-gradient(to right, var(--va-background-primary), var(--va-white));
    // background-color: #001a5a;

    &__card {
      width: 100%;
      max-width: 600px;
    }
  }

  #myVideo {
    position: fixed;
    right: 0;
    bottom: 0;
    min-width: 100%;
    min-height: 100%;
    z-index: -1;
    opacity: 0.9;
  }

  .titleen {
    font-size: 20px;
  }

  .titlecn {
    font-size: 70px;
    color: #15e8ef;
    width: 600px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
  }

  .bgpic1 {
    position: fixed;
    left: -200px;
    top: 60px;
    width: 768px;
  }

  .bgpic2 {
    position: fixed;
    right: -200px;
    top: 60px;
    width: 768px;
  }

  .bgpic4 {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 268px;
  }
</style>
