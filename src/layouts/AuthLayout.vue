<template>
  <div class="auth-layout row align-content-center" style="height: 780px; width: 1480px">
    <img class="bgpic1" src="../../public/bgpic1.png" alt="" />
    <img class="bgpic2" src="../../public/bgpic2.png" alt="" />
    <img class="bgpic4" src="../../public/bgpic4.png" alt="" />
    <div class="toplefttip">意见反馈</div>
    <div class="toprighttip">关于我们</div>
    <div class="flex xs12 pa-3 justify-center">
      <router-link class="py-5 justify-center d-flex" to="/">
        <div style="text-align: center; color: #fff">
          <h1 class="titleen">Bus Driver Safety Digital Portrait System</h1>
          <h1 class="titlecn">公交驾驶员行车安全数字画像系统</h1>
        </div>
        <!-- <vuestic-logo height="32" /> -->
      </router-link>
    </div>

    <div class="flex xs12 pa-3">
      <div class="d-flex justify-center">
        <img class="bgpic3" src="../../public/bgpic3.png" alt="" />
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
    background-image: linear-gradient(to right, var(--va-background-primary), var(--va-white));
    background-color: #001a5a;

    &__card {
      width: 100%;
      max-width: 600px;
    }
  }

  .titleen {
    font-size: 20px;
  }

  .titlecn {
    font-size: 70px;
    color: #75f9fd;
    width: 600px;
  }

  .bgbox1 {
    position: absolute;
    left: -8px;
    top: 0px;
    width: 1664px;
    height: 223px;
    line-height: 20px;
    border-radius: 0px 10px 10px 0px;
    background: linear-gradient(86.79deg, rgba(9, 15, 150, 1) 2.5%, rgba(0, 127, 252, 1) 97.29%);
    text-align: center;
  }

  .bgpic1 {
    position: fixed;
    left: -200px;
    top: 90px;
    width: 768px;
    // height: 208px;
  }

  .bgpic2 {
    position: fixed;
    right: -200px;
    top: 90px;
    width: 768px;
    // height: 341px;
  }

  .toplefttip {
    position: fixed;
    left: 0;
    top: 0;
    color: #fff;
    margin-left: 20px;
    margin-top: 10px;
    text-decoration: underline;
  }

  .toprighttip {
    position: fixed;
    right: 0;
    top: 0;
    color: #fff;
    margin-right: 20px;
    margin-top: 10px;
    text-decoration: underline;
  }

  .bgpic3 {
    width: 300px;
    height: 300px;
    margin-right: 100px;
  }

  .bgpic4 {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 268px;
    // height: 768px;
  }
</style>
