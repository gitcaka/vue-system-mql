<template>
  <div class="row">
    <div class="flex xl8">
      <va-card style="height: 100%">
        <va-card-title style="justify-content: space-between">
          <h1 style="font-size: 20px">乘客反馈</h1>
        </va-card-title>
        <va-card-content>
          <h1 style="font-size: 14px; font-weight: normal">
            系统通过整理乘客在公交驾驶员行车安全方面的意见以及建议，
            更加直观、客观、全面描述公交驾驶员行车安全数字画像。
          </h1>
        </va-card-content>
      </va-card>
    </div>

    <div class="flex xl4">
      <va-card style="height: 100%">
        <va-card-title>
          <h1>最近更新时间</h1>
        </va-card-title>
        <va-card-content>
          <div style="display: flex;i;justify-content: space-between;align-items: center;">
            <h1>{{ currentTime }} {{ dayOfWeek }}</h1>
            <div style="display: flex">
              <div class="ma-1" style="display: flex; align-items: center">
                <va-button icon="ion-ios-refresh" plain @click="refresh"></va-button>
                <p>刷新</p>
              </div>
              <div class="ma-1" style="display: flex; align-items: center">
                <va-button icon="more_horiz" plain @click="refresh"></va-button>
                <p>反馈</p>
              </div>
            </div>
          </div>
        </va-card-content>
      </va-card>
    </div>
  </div>

  <va-card class="mt-3">
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">平台评价信息</h1>
    </va-card-title>
    <va-card-content>
      <div class="row" style="align-items: center">
        <div class="flex xs5" style="border-right: 1px solid #9ba4b4">
          <div class="va-h6 ma-0 row" style="align-items: center; justify-content: center">
            <img class="ma-2" src="../../../public/weibo.png" style="height: 48px; width: 48px" />
            <p>新浪微博</p>
          </div>
          <p class="va-text-center">
            平台地址：<a href="https://weibo.com/u/2486101491">https://weibo.com/u/2486101491</a>
          </p>
        </div>
        <div class="xs7" style="display: flex; align-items: center; padding-left: 20px">
          <img class="ma-3" src="../../../public/zhihu.png" style="height: 48px; width: 48p" />
          <img class="ma-3" src="../../../public/douyin.png" style="height: 48px; width: 48px" />
          <img class="ma-3" src="../../../public/blibli.png" style="height: 48px; width: 48px" />
          <img class="ma-3" src="../../../public/txweibo.png" style="height: 48px; width: 48px" />
          <img class="ma-3" src="../../../public/tieba.png" style="height: 48px; width: 48px" />
          <img class="ma-3" src="../../../public/wxxiaochenxu.png" style="height: 48px; width: 48px" />
          <img class="ma-3" src="../../../public/pinglun.png" style="height: 48px; width: 48px" />
          <img class="ma-3" src="../../../public/more.png" style="height: 40px; width: 40px" />
        </div>
      </div>
    </va-card-content>
  </va-card>

  <va-card class="mt-4">
    <va-card-content>
      <div style="display: flex; font-size: 20px; align-items: center; width: 100%">
        <va-icon name="ion-ios-arrow-back" style="color: #1e9fff; font-size: 25px; margin-right: 10px" />
        <h1>当前选择</h1>
        <h1 style="color: #158de3; margin-left: 10px">推文评论-重庆公交-2023年5月10日</h1>
        <va-select
          v-model="selectModal"
          text-by="description"
          track-by="id"
          :options="selectOptions"
          style="width: 20%; margin: 0 10px"
        />
        <va-input v-model="search" placeholder="输入关键字查询" clearable>
          <template #prependInner>
            <va-icon class="icon-left input-icon" name="search" />
          </template>
        </va-input>
      </div>
    </va-card-content>
  </va-card>

  <div class="row" style="height: 100%">
    <div class="flex xs5" style="height: 100%">
      <va-card style="height: 100%">
        <va-card-content>
          <img src="../../../public/swiper1.png" style="width: 100%" />
          <!-- <Swiper :params="swiperOptions" style="width: 100%; overflow: hidden">
            <SwiperSlide v-for="(slide, index) in swiperSlides" :key="index" style="">
              <img :src="slide.image" style="width: 100%" />
            </SwiperSlide>
          </Swiper> -->
        </va-card-content>
      </va-card>
    </div>

    <div class="flex xs7" style="height: auto">
      <va-card style="height: 100%">
        <va-card-content>
          <va-list class="">
            <va-list-label> 平台评价展示 </va-list-label>
            <template v-for="(customer, i) in comments" :key="'item' + customer.id">
              <va-list-item style="padding: 2px 0">
                <va-list-item-section avatar>
                  <va-avatar>
                    <img :src="customer.picture" :alt="customer.name" />
                  </va-avatar>
                </va-list-item-section>
                <va-list-item-section>
                  <va-list-item-label caption> {{ customer.name }} </va-list-item-label>
                  <va-list-item-label> {{ customer.content }} </va-list-item-label>
                </va-list-item-section>
              </va-list-item>
              <va-list-separator v-if="i < comments.length - 1" :key="'separator' + customer.id" class="my-1" fit />
            </template>
          </va-list>
        </va-card-content>
      </va-card>
    </div>
  </div>

  <va-card>
    <va-card-title style="display: flex; justify-content: center">
      <h1 class="headTitle">评价词云分析</h1>
    </va-card-title>
    <va-card-content style="line-height: 1.5">
      <h1 style="color: rgb(21, 78, 193); margin: 0 0 10px 0; font-size: 20px">概述</h1>
      <p>评论者对公交的评价分为两类：积极正面的评价和消极负面的评价。<br /></p>
      <p style="color: #3d9209">积极正面评价</p>
      <p>
        有些评论者认为新开通的公交线路很方便且到达目的地速度快，司机态度好且细心地帮助乘客坐好，乘车流畅，驾驶员的技术扎实。
      </p>
      <p style="color: #e42222">消极负面评价</p>
      <p style="margin-bottom: 10px">
        一些评论者认为公交车速太慢、人流较多、空间拥挤以及司机的驾驶不安全等问题；还有一些评论者认为公交经常超载、车站拥挤影响乘车体验、座位设计不符合人体工程学、停靠位置不合理等问题。
      </p>
      <h1 style="color: rgb(21, 78, 193); padding: 10px 0 10px 0; font-size: 20px; border-top: gray 1px solid">建议</h1>
      <p style="line-height: 1.5">
        建议主要是公交公司要加强管理监管、提高服务水平等。总体来说，公共交通是城市基础设施之一，为市民生活带来方便，但也需要更好的管理和规划才能更好地服务市民。
      </p>
      <p style="text-align: end; color: #158de3; text-decoration: underline">查看更多</p>
    </va-card-content>
  </va-card>

  <va-card class="mt-4">
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">乘客反馈信息</h1>
    </va-card-title>
    <va-card-content>
      <div style="display: flex; align-items: center; justify-content: center">
        <va-select
          v-model="yearModal"
          class="mr-2"
          text-by="description"
          track-by="id"
          :options="yearOptions"
          style="width: 20%"
        />
        <va-select
          v-model="quarterModal"
          class="mr-2"
          text-by="description"
          track-by="id"
          :options="quarterOptions"
          style="width: 20%"
        />
        <va-select
          v-model="monthModal"
          text-by="description"
          track-by="id"
          :options="monthOptions"
          style="width: 20%"
        />
      </div>
    </va-card-content>
  </va-card>

  <div class="row" style="height: 100%">
    <div class="flex xs6" style="height: 100%">
      <va-card style="height: 100%">
        <va-card-title>
          <h1 class="headTitle">乘客反馈统计</h1>
        </va-card-title>
        <va-card-content style="align-items: center; text-align: center">
          <h1 class="va-h6 ma-3">2022年平台受理乘客投诉渠道分布图</h1>
          <img class="chartimg" src="../../../public/feedbackpic1.png" />
          <h1 class="va-h6 ma-3" style="border-top: 1px solid gray; padding-top: 10px">2022年受理投诉统计图（季度）</h1>
          <img class="chartimg" src="../../../public/feedbackpic2.png" />
          <div style="width: 100%; justify-content: center; display: flex; margin-top: 20px">
            <va-pagination v-model="activePage1" :visible-pages="4" :pages="20" />
          </div>
        </va-card-content>
      </va-card>
    </div>

    <div class="flex xs6" style="height: auto">
      <va-card style="height: 100%">
        <va-card-title>
          <h1 class="headTitle">司机行车安全服务质量信息</h1>
        </va-card-title>
        <va-card-content style="text-align: center">
          <div>
            <h1 class="va-h6 ma-3">2022年度司机行车安全服务质量影响因素统计表</h1>
            <img src="../../../public/feedbackpic3.png" style="width: 100%" />
            <h1 class="va-h6 ma-3">2022年司机优质服务记录</h1>
            <img class="feedback4" src="../../../public/feedbackpic4.png" />
          </div>
          <div style="width: 100%; justify-content: center; display: flex; position: absolute; bottom: 20px">
            <va-pagination v-model="activePage2" :visible-pages="4" :pages="20" />
          </div>
        </va-card-content>
      </va-card>
    </div>
  </div>

  <va-card class="mt-3">
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">司机服务质量信息查询</h1>
    </va-card-title>
    <va-card-content>
      <div style="display: flex; align-items: center">
        <va-input v-model="search" placeholder="请输入驾驶员姓名" clearable style="margin: 10px 10px 10px 0">
          <template #prependInner>
            <va-icon class="icon-left input-icon" name="search" />
          </template>
        </va-input>

        <va-input v-model="search" placeholder="请输入驾驶员工号" clearable style="margin: 10px 10px 10px 0">
          <template #prependInner>
            <va-icon class="icon-left input-icon" name="search" />
          </template>
        </va-input>
      </div>

      <div class="table-wrapper">
        <table class="va-table va-table--striped va-table--hoverable" style="width: 100%; color: #000">
          <thead>
            <tr>
              <th>工号</th>
              <th>姓名</th>
              <th>驾驶车牌号</th>
              <th>线路</th>
              <th>驾驶员健康</th>
              <th>驾驶员行为</th>
              <th>驾驶员技能</th>
              <th>预警状态</th>
              <th>数字画像总评分</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="user in driverInfos" :key="user.id">
              <td>{{ user.id }}</td>
              <td>{{ user.name }}</td>
              <td>{{ user.carNum }}</td>
              <td>{{ user.line }}</td>
              <td><va-badge :text="user.health" :color="getStatusColor(user.health)" /></td>
              <td><va-badge :text="user.behavior" :color="getStatusColor(user.behavior)" /></td>
              <td><va-badge :text="user.skill" :color="getStatusColor(user.skill)" /></td>
              <td><va-badge :text="user.status" :color="getStatusColor(user.status)" /></td>
              <td><va-badge :text="user.score" :color="getScoreColor(user.score)" /></td>
            </tr>
          </tbody>
        </table>
      </div>
      <div style="width: 100%; justify-content: center; display: flex; margin-top: 20px">
        <va-pagination v-model="activeTable" :visible-pages="10" :pages="99" />
      </div>
    </va-card-content>
  </va-card>

  <swiper :pagination="{ clickable: true }">
    <swiper-slide>Slide 1</swiper-slide>
    <swiper-slide>Slide 2</swiper-slide>
    <swiper-slide>Slide 3</swiper-slide>
  </swiper>
</template>

<script setup lang="ts">
  import { ref } from 'vue'

  const currentTime = ref(new Date().toLocaleString().split(' ')[0])
  const dayOfWeek = new Intl.DateTimeFormat('zh-CN', { weekday: 'long' }).format(new Date())
  const selectModal = ref('推文评论')
  const yearModal = ref('2022')
  const quarterModal = ref('全部')
  const monthModal = ref('全部')
  const activePage1 = ref(1)
  const activePage2 = ref(1)
  const activeTable = ref(1)
  const monthOptions = ref([
    { id: 1, description: '1月' },
    { id: 2, description: '2月' },
    { id: 3, description: '3月' },
    { id: 4, description: '4月' },
    { id: 5, description: '5月' },
    { id: 6, description: '6月' },
    { id: 7, description: '7月' },
    { id: 8, description: '8月' },
    { id: 9, description: '9月' },
    { id: 10, description: '10月' },
    { id: 11, description: '11月' },
    { id: 12, description: '12月' },
  ])
  const quarterOptions = ref([
    { id: 1, description: '第一季度' },
    { id: 2, description: '第二季度' },
    { id: 3, description: '第三季度' },
    { id: 4, description: '第四季度' },
  ])
  const yearOptions = ref([
    { id: 1, description: '2022' },
    { id: 2, description: '2019' },
    { id: 3, description: '2018' },
    { id: 4, description: '2017' },
  ])
  const selectOptions = ref([
    { id: 1, description: '推文评论' },
    { id: 2, description: '微博' },
    { id: 3, description: '知乎' },
    { id: 4, description: '抖音' },
    { id: 5, description: 'B站' },
    { id: 6, description: '贴吧' },
  ])
  const search = ref('')
  //   const swiperOptions = ref({
  //     spaceBetween: 10,
  //     slideClass: 'custom-slide-class',
  //     pagination: {
  //       el: '.swiper-pagination', //与slot="pagination"处 class 一致
  //       clickable: true, //轮播按钮支持点击
  //     },
  //     autoplay: {
  //       delay: 100,
  //       disableOnInteraction: false,
  //     },
  //     loop: true,
  //   })
  // const swiperSlides = ref([{ image: '../../../public/swiper1.png' }, { image: '../../../public/swiper2.png' }])
  const comments = ref([
    {
      id: 1,
      name: '康康',
      content: '乘客物品遗落在哪里找?',
      picture: 'https://img1.baidu.com/it/u=1403245892,3051757811&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
    },
    {
      id: 2,
      name: '小欣儿',
      content: '到晚上18点轮班之前，驾驶员开车比较拥挤，肆意压挤其他车辆，不安全！',
      picture: 'https://img1.baidu.com/it/u=2961575590,2057372040&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
    },
    {
      id: 3,
      name: '方上有🐟富',
      content:
        '昨天乘坐19路，上车后发现司机态度很好，细心询问我要去的地方，直接引导我到位子上坐好，整个过程让我感觉很温暖[赞]',
      picture: 'https://img2.baidu.com/it/u=1684676393,4028279466&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
    },
    {
      id: 4,
      name: '西敏Love',
      content: '便民服务[good]',
      picture: 'https://img0.baidu.com/it/u=2066003044,2169631129&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
    },
    {
      id: 5,
      name: '社会你杰哥',
      content: '[打call][打call]👀',
      picture: 'https://img2.baidu.com/it/u=962524885,1917877329&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
    },
    {
      id: 6,
      name: '胡小宝',
      content: '暖心公交[赞][赞][赞]',
      picture: 'https://img1.baidu.com/it/u=3436323259,1946271733&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
    },
  ])

  const driverInfos = ref([
    {
      id: '0452',
      name: '张权',
      carNum: '渝A9167D',
      line: '16,21',
      health: '中',
      behavior: '优',
      skill: '中',
      status: '安全',
      score: '81',
    },
    {
      id: '0453',
      name: '张新华',
      carNum: '渝AYT003',
      line: '24',
      health: '中',
      behavior: '中',
      skill: '中',
      status: '警告',
      score: '67',
    },
    {
      id: '0454',
      name: '张婷婷',
      carNum: '渝AD862Y',
      line: '5',
      health: '优',
      behavior: '中',
      skill: '优',
      status: '安全',
      score: '83',
    },
    {
      id: '0455',
      name: '张军',
      carNum: '渝A7RH64',
      line: '16,21',
      health: '优',
      behavior: '差',
      skill: '中',
      status: '危险',
      score: '64',
    },
    {
      id: '0456',
      name: '张美琳',
      carNum: '渝AERS6',
      line: '16,21',
      health: '中',
      behavior: '优',
      skill: '中',
      status: '安全',
      score: '78',
    },
    {
      id: '0457',
      name: '张静',
      carNum: '渝A6EF51',
      line: '16,21',
      health: '优',
      behavior: '优',
      skill: '优',
      status: '安全',
      score: '93',
    },
    {
      id: '0458',
      name: '张亚文',
      carNum: '渝ADF54D',
      line: '5',
      health: '优',
      behavior: '中',
      skill: '优',
      status: '安全',
      score: '87',
    },
    {
      id: '0459',
      name: '张新华',
      carNum: '渝AYT003',
      line: '24,102',
      health: '中',
      behavior: '中',
      skill: '中',
      status: '警告',
      score: '67',
    },
    {
      id: '0460',
      name: '张权',
      carNum: '渝A9167D',
      line: '5',
      health: '中',
      behavior: '优',
      skill: '中',
      status: '安全',
      score: '81',
    },
    {
      id: '0461',
      name: '张新华',
      carNum: '渝AYT003',
      line: '16,21',
      health: '中',
      behavior: '中',
      skill: '中',
      status: '警告',
      score: '67',
    },
    {
      id: '0462',
      name: '张权',
      carNum: '渝A9167D',
      line: '24',
      health: '中',
      behavior: '优',
      skill: '中',
      status: '安全',
      score: '81',
    },
    {
      id: '0463',
      name: '张新华',
      carNum: '渝AYT003',
      line: '5',
      health: '中',
      behavior: '中',
      skill: '中',
      status: '警告',
      score: '67',
    },
    {
      id: '0464',
      name: '张权',
      carNum: '渝A9167D',
      line: '24',
      health: '中',
      behavior: '优',
      skill: '中',
      status: '安全',
      score: '81',
    },
    {
      id: '0465',
      name: '张新华',
      carNum: '渝AYT003',
      line: '24,102',
      health: '中',
      behavior: '中',
      skill: '中',
      status: '警告',
      score: '67',
    },
    {
      id: '0466',
      name: '李明',
      carNum: '渝A1234B',
      line: '24,102',
      health: '中',
      behavior: '中',
      skill: '中',
      status: '安全',
      score: '75',
    },
    {
      id: '0467',
      name: '李华',
      carNum: '渝A5678C',
      line: '24,102',
      health: '中',
      behavior: '优',
      skill: '中',
      status: '警告',
      score: '68',
    },
    {
      id: '0468',
      name: '李雷',
      carNum: '渝A9012D',
      line: '24,102',
      health: '中',
      behavior: '差',
      skill: '中',
      status: '危险',
      score: '62',
    },
    {
      id: '0469',
      name: '李芳',
      carNum: '渝A3456E',
      line: '24,102',
      health: '优',
      behavior: '中',
      skill: '优',
      status: '安全',
      score: '89',
    },
  ])

  function getStatusColor(status: string) {
    if (['安全', '优'].includes(status)) {
      return 'success'
    } else if (['警告', '中'].includes(status)) {
      return 'warning'
    } else return 'danger'
  }

  function getScoreColor(score: string) {
    let scoreNum = Number(score)
    if (scoreNum > 70) {
      return 'success'
    } else if (scoreNum >= 65) {
      return 'warning'
    } else return 'danger'
  }
  function refresh() {
    console.log(111)
  }
</script>

<style>
  .custom-slide-class {
    width: 100%;
    height: 100%;
  }

  .headTitle {
    font-size: 1rem;
    letter-spacing: 0.6px;
    line-height: 1.2;
    font-weight: 700;
    color: rgb(21, 78, 193);
  }

  .chartimg {
    background-color: #001a5a;
    width: 100%;
    padding: 30px 0 20px 0;
    border-radius: 20px;
  }

  .feedback4 {
    width: 100%;
    background-color: #001a5a;
    padding: 25px 10px 0 10px;
    border-radius: 10px;
  }

  .va-table th {
    text-align: center;
  }

  .va-table td {
    text-align: center;
  }
</style>
