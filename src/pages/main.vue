<template>
  <div class="" style="background-color: #001a5a; height: 780px; width: 1480px">
    <div class="top row">
      <img class="bgpic5" src="../../public/bgpic5.png" alt="" />
      <img class="bgpic6" src="../../public/bgpic6.png" alt="" />
      <div class="tleft row grid__container">
        <va-icon name="access_time" style="color: #1e9fff" />
        <p style="color: #fff; margin-left: 5px">{{ currentTime }} &nbsp; {{ dayOfWeek }}</p>
      </div>
      <div class="row grid__container">
        <div class="tcenter">
          <h1 class="title1">公交驾驶员行车安全数字画像系统</h1>
          <h1 class="title2">数据可视化平台</h1>
        </div>
        <img class="bgpic3" src="../../public/bgpic3.png" alt="" />
      </div>
      <div class="row grid__container">
        <div class="tright">
          <p class="titleright1">重庆两江公共交通有限公司</p>
          <div style="display: flex">
            <va-icon :name="tianqiIcon" style="color: #1e9fff; margin-right: 10px" />
            <p class="titleright1">{{ wendu }} &nbsp; &nbsp; {{ tianqi }} &nbsp; &nbsp; &nbsp; &nbsp; 重庆市</p>
          </div>
        </div>
      </div>
    </div>
    <div class="bottom">
      <div class="bleft">
        <div class="bltop blboxs" style="height: 180px">
          <div style="display: flex; justify-content: space-between">
            <p style="font-size: 18px; color: #fff">今日违规统计</p>
            <p style="font-size: 18px; color: #71eef3">关联性分析</p>
          </div>
          <div class="gird1">
            <div v-for="(item, index) in violationData" :key="index" class="bltgird">
              <p style="color: #71eef3; font-size: 20px; font-weight: bold">{{ item.num }}</p>
              <p class="gird1title">{{ item.title }}</p>
            </div>
          </div>
        </div>
        <div class="blcenter blboxs">
          <div class="row" style="justify-content: space-between">
            <p style="font-size: 18px; color: #fff">今日显著聚类预警</p>
            <p style="font-size: 18px; color: #71eef3">司机画像聚类</p>
          </div>
          <div style="display: flex; height: 135px; overflow: hidden">
            <va-card style="background-color: initial; box-shadow: none; position: relative; top: -80px">
              <va-card-content>
                <va-chart :data="doughnutChartDataGenerated" type="doughnut" />
              </va-card-content>
            </va-card>
            <va-card style="background-color: initial; box-shadow: none; color: #fff; position: relative">
              <va-card-content style="display: flex; flex-direction: column; align-items: center">
                <div class="mb-3" style="width: 120px">
                  <va-progress-bar model-value="80" color="danger">状态差:80% </va-progress-bar>
                </div>
                <div class="mb-3" style="width: 120px">
                  <va-progress-bar model-value="20" color="primary">状态正常:20% </va-progress-bar>
                </div>
              </va-card-content>
            </va-card>
          </div>
        </div>
        <div class="blright blboxs">
          <div class="row" style="justify-content: space-between; width: 100%">
            <p style="font-size: 18px; color: #fff">预警司机实时监控</p>
            <p style="font-size: 18px; color: #71eef3">详情</p>
          </div>
          <div class="mt-2" style="display: flex; justify-content: space-around">
            <div style="">
              <div style="display: flex; font-weight: bold; margin-bottom: 8px; margin-top: 2px">
                <p style="color: #fff">张权 ----- &nbsp;</p>
                <p style="color: red">危险预警</p>
              </div>
              <div style="display: flex; flex-direction: column; width: 200px">
                <video src="../../public/video1.mp4" autoplay muted loop style="margin-bottom: 5px"></video>
                <video src="../../public/video2.mp4" autoplay muted loop></video>
              </div>
            </div>
            <div style="display: flex; flex-direction: column">
              <va-chip shadow class="mb-2" color="primary" style="font-size: 12px">未系安全带</va-chip>
              <va-chip shadow class="mb-2" color="secondary" style="font-size: 12px">离开方向盘</va-chip>
              <va-chip shadow class="mb-2" color="success" style="font-size: 12px">疲劳驾驶</va-chip>
              <va-chip shadow class="mb-2" color="info" style="font-size: 12px">分心驾驶</va-chip>
              <va-chip shadow class="mb-2" color="danger" style="font-size: 12px">跟车太近</va-chip>
              <va-chip shadow class="mb-2" color="warning" style="font-size: 12px">与乘客交谈</va-chip>
              <va-chip shadow class="mb-2" color="gray" style="font-size: 12px">离开驾驶位</va-chip>
              <va-chip shadow class="mb-2" color="dark" style="font-size: 12px">离开方向盘</va-chip>
            </div>
          </div>
        </div>
      </div>
      <div class="bcenter">
        <div class="bctop">
          <div class="bctopmain" style="display: flex">
            <div v-for="(item, index) in bctopData" :key="index" class="bctopblock">
              <div class="row" style="align-items: center; font-size: 10px">
                <va-icon :name="item.icon" style="color: #1e9fff" />
                <div style="color: #fff">{{ item.title }}</div>
              </div>
              <div>
                <div class="bctnum">
                  {{ item.num }}
                  <va-icon v-if="item.ifadd" :name="item.addIcon" style="color: #1e9fff; margin-left: 10px" />
                  {{ item.addnum }}
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="bccenter mt-3">
          <baidu-map
            center="重庆"
            :zoom="zoom"
            :scroll-wheel-zoom="true"
            :map-click="false"
            style="width: 100%; height: 433px"
            @ready="mapReadyHandler"
          >
            <bm-marker
              v-for="item in markers"
              :key="item.id"
              :position="{ lng: item.location[0], lat: item.location[1] }"
              :icon="{ url: item.icon, size: { width: 64, height: 64 } }"
              @click="clickMarker(item)"
            >
            </bm-marker>
            <bm-info-window :show="infoShow" :position="infoPosition" @open="infoWindowOpen" @close="infoWindowClose"
              >{{ infoContent }}
            </bm-info-window>
            <!-- <bm-traffic> </bm-traffic> -->
            <bm-geolocation
              anchor="BMAP_ANCHOR_BOTTOM_RIGHT"
              :show-address-bar="false"
              :auto-location="true"
            ></bm-geolocation>
          </baidu-map>
          <!-- <img src="../../public/swaper.png" style="width: 100%" alt="" /> -->
        </div>
        <div class="bcbottom">
          <div class="bcbleft bcbbox">
            <div class="row" style="justify-content: space-between; width: 100%">
              <p style="font-size: 18px; color: #fff">考核优秀人数</p>
              <p style="font-size: 18px; color: #71eef3"></p>
            </div>
            <div v-for="(item, index) in bcbleftData" :key="index" class="bcbleftfor">
              <div class="mytag" :style="'background-color: ' + item.color">{{ index + 1 }}</div>
              <div class="bcbtitle">{{ item.title }}</div>
              <va-progress-bar :model-value="(item.num / bcbleftTotalNum) * 100" />
              <div style="color: #fff; font-size: 15px; margin-left: 5px">{{ item.num }}</div>
            </div>
          </div>
          <div class="bcbright bcbbox">
            <div class="row" style="justify-content: space-between; width: 100%">
              <p style="font-size: 18px; color: #fff">考核不合格人数</p>
              <p style="font-size: 18px; color: #71eef3">考核方案优化</p>
            </div>
            <div v-for="(item, index) in bcbrightData" :key="index" class="bcbleftfor">
              <div class="mytag" :style="'background-color: ' + item.color">{{ index + 1 }}</div>
              <div class="bcbtitle">{{ item.title }}</div>
              <va-progress-bar :model-value="(item.num / bcbleftTotalNum) * 100" />
              <div style="color: #fff; font-size: 15px; margin-left: 5px">{{ item.num }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="bright">
        <div class="brtop brbbox">
          <div class="row" style="justify-content: space-between; width: 100%">
            <p style="font-size: 18px; color: #fff">司机当前状况及预警</p>
            <router-link to="/admin/drivers">
              <div style="display: flex">
                <p style="font-size: 18px; color: #71eef3">详情</p>
                <va-icon name="chevron_right" style="color: #1e9fff" />
              </div>
            </router-link>
          </div>
          <table class="va-table">
            <thead>
              <tr>
                <th>姓名</th>
                <th>工号ID</th>
                <th>健康素质</th>
                <th>驾驶行为</th>
                <th>驾驶技能</th>
                <th>预警状态</th>
                <th>总分</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="user in tableData" :key="user.id">
                <td>{{ user.name }}</td>
                <td>{{ user.id }}</td>
                <td>{{ user.health }}</td>
                <td>{{ user.behavior }}</td>
                <td>{{ user.skill }}</td>
                <td>{{ user.status }}</td>
                <td>{{ user.score }}</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="brbottom brbbox">
          <div class="row" style="justify-content: space-between; width: 100%">
            <p style="font-size: 18px; color: #fff">内部团队在编人数</p>
            <p style="font-size: 18px; color: #71eef3">人员基本档案</p>
          </div>
          <div style="display: flex; width: 100%; margin-top: 10px; justify-content: space-around">
            <va-card color="success" style="width: 48%">
              <va-card-content>
                <p style="color: white; font-size: 14px">行驶中</p>
                <h2 style="color: white; font-size: 41px">467</h2>
                <p style="color: white; font-size: 12px">月离职人数: 8 9.52%</p>
              </va-card-content>
            </va-card>
            <va-card color="info" style="width: 48%">
              <va-card-content>
                <p style="color: white; font-size: 14px">总人数</p>
                <h2 style="color: white; font-size: 41px">1239</h2>
                <p style="color: white; font-size: 12px">月离职人数: 8 10%</p>
              </va-card-content>
            </va-card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { onMounted, ref } from 'vue'
  import { useChartData } from '../data/charts/composables/useChartData'
  import VaChart from '../components/va-charts/VaChart.vue'
  import axios from 'axios'
  import qs from 'qs'

  const currentTime = ref(new Date().toLocaleString())
  const updateTime = () => {
    currentTime.value = new Date().toLocaleString()
  }
  const dayOfWeek = new Intl.DateTimeFormat('zh-CN', { weekday: 'long' }).format(new Date())
  // const cityName = ref('')
  const wendu = ref('')
  const tianqi = ref('')
  const tianqiIcon = ref('')
  const violationData = ref([
    { title: '错误驾驶', num: 182 },
    { title: '失误驾驶', num: 233 },
    { title: '违规驾驶', num: 343 },
    { title: '攻击性驾驶', num: 382 },
    { title: '车速异常', num: 423 },
    { title: '车距异常', num: 535 },
    { title: '平稳性异常', num: 675 },
    { title: '预警司机比例', num: '35%' },
  ])
  const bctopData = ref([
    { title: '司机总人数', num: 1239, ifadd: false, addnum: 0, icon: 'person_outline', addIcon: '' },
    { title: '今日预警数', num: 2232, ifadd: true, addnum: 231, icon: 'warning', addIcon: 'entypo-up-thin' },
    { title: '近期身体健康预警', num: '26%', ifadd: true, addnum: '3%', icon: 'check', addIcon: 'entypo-up-thin' },
    {
      title: '近期驾驶行为预警',
      num: '67%',
      ifadd: true,
      addnum: '2%',
      icon: 'directions_run',
      addIcon: 'entypo-up-thin',
    },
    {
      title: '近期驾驶员技术预警',
      num: '43%',
      ifadd: true,
      addnum: '4%',
      icon: 'event_note',
      addIcon: 'entypo-up-thin',
    },
  ])
  const tableData = ref([
    { name: '艾一宁', id: '0216', health: '优', behavior: '优', skill: '差', status: '危险', score: 62 },
    { name: '安艳', id: '9654', health: '优', behavior: '中', skill: '优', status: '安全', score: 88 },
    { name: '安成耀', id: '3902', health: '优', behavior: '优', skill: '优', status: '安全', score: 96 },
    { name: '包睿', id: '4678', health: '优', behavior: '中', skill: '优', status: '警告', score: 81 },
    { name: '包文凯', id: '4892', health: '中', behavior: '中', skill: '差', status: '警告', score: 56 },
    { name: '曹清文', id: '6327', health: '优', behavior: '优', skill: '中', status: '安全', score: 90 },
    { name: '曹友荃', id: '2259', health: '优', behavior: '优', skill: '优', status: '安全', score: 95 },
    { name: '曹光', id: '7631', health: '优', behavior: '优', skill: '中', status: '安全', score: 89 },
    { name: '陈艺星', id: '0832', health: '中', behavior: '中', skill: '优', status: '警告', score: 73 },
    { name: '陈真', id: '1678', health: '差', behavior: '中', skill: '优', status: '警告', score: 68 },
  ])
  const doughnutChartDataGenerated = useChartData({
    labels: ['身体健康状态正常', '身体健康状态差'],
    datasets: [
      {
        label: '健康状态',
        backgroundColor: ['info', 'danger'],
        data: [61, 245],
      },
    ],
  })

  // const center = ref({ lng: 116.404, lat: 39.915 })
  const zoom = ref(13)
  // const markerPoint = ref({ lng: 106.531869, lat: 29.594114 })
  const markers = ref([
    { id: 1, location: [106.540205, 29.557017], content: '第一个点', icon: '../../public/point_default.png' },
    { id: 2, location: [106.555368, 29.567196], content: '第二个点', icon: '../../public/point_blue.png' },
    { id: 3, location: [106.574772, 29.540867], content: '第三个点', icon: '../../public/point_red.png' },
    { id: 4, location: [106.490116, 29.585729], content: '第四个点', icon: '../../public/point_yellow.png' },
    { id: 5, location: [106.60323, 29.580829], content: '第五个点', icon: '../../public/point_green.png' },
    { id: 6, location: [106.557812, 29.611229], content: '第六个点', icon: '../../public/point_darkblue.png' },
    { id: 7, location: [106.637438, 29.566002], content: '第七个点', icon: '../../public/point_purple.png' },
  ])
  const infoShow = ref(false)
  const infoContent = ref('')
  const infoPosition = ref()
  const infoWindowOpen = ref(function () {
    infoShow.value = true
  })
  const infoWindowClose = ref(function () {
    infoShow.value = false
  })
  const mapReadyHandler = ref(function ({ map }) {
    let mapStyle = { style: 'bluish' }
    map.setMapStyle(mapStyle)
    // map.setMapStyleV2({
    //   styleId: '92e4203b695ec4c9f650eaf20ef61d58',
    // })
  })
  const clickMarker = ref(function (item: { location: any[]; content: string }) {
    infoPosition.value = { lng: item.location[0], lat: item.location[1] }
    // console.log(infoPosition.value, item.icon)
    infoContent.value = item.content
    infoShow.value = true
  })

  const bcbleftData = ref([
    { title: '心理健康', num: 2000, color: '#E42222' },
    { title: '攻击性驾驶', num: 1800, color: '#ff842b' },
    { title: '违规驾驶', num: 1600, color: '#FFD43A' },
    { title: '疾病史', num: 1500, color: '#8f4ed6' },
    { title: '疲劳驾驶', num: 1400, color: '#158DE3' },
  ])
  const bcbleftTotalNum = ref(bcbleftData.value.reduce((acc, cur) => acc + cur.num, 0) / 2)

  const bcbrightData = ref([
    { title: '失误驾驶', num: 2000, color: '#E42222' },
    { title: '平稳性异常', num: 1800, color: '#ff842b' },
    { title: '车速异常', num: 1600, color: '#FFD43A' },
    { title: '健康意识', num: 1500, color: '#8f4ed6' },
    { title: '车距异常', num: 1400, color: '#158DE3' },
  ])

  onMounted(() => {
    setInterval(updateTime, 1000)

    axios({
      method: 'post',
      url: 'https://apis.tianapi.com/tianqi/index',
      data: qs.stringify({ key: '89fd8002d6d9b3ba7c3c98748efa2779', city: '重庆市', type: '1' }),
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
    }).then((res) => {
      // console.log(res.data.result)
      wendu.value = res.data.result.lowest + ' - ' + res.data.result.highest
      tianqi.value = res.data.result.weather
      if (tianqi.value.indexOf('云') !== -1) {
        tianqiIcon.value = 'cloud'
      } else {
        tianqiIcon.value = 'md-sunny'
      }
    })
  })
</script>

<style>
  .bgpic5 {
    position: absolute;
    top: 0;
    left: 0px;
    height: 80px;
    width: auto;
  }

  .bgpic6 {
    position: absolute;
    top: 0;
    right: 0px;
    height: 80px;
    width: auto;
  }

  .tleft {
    margin: 38px 0 0 40px;
  }

  .title1 {
    font-size: 25px;
    color: #75f9fd;
    text-align: center;
  }

  .tcenter {
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 10px 0 0 200px;
  }

  .title2 {
    font-size: 30px;
    color: white;
    text-align: center;
  }

  .bgpic3 {
    height: 80px;
    width: auto;
    margin-left: 10px;
  }

  .tright {
    margin: 30px 0 0 150px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }

  .titleright1 {
    color: white;
    margin-left: 20px;
    margin: 0 0 5px 0;
  }

  .bottom {
    display: flex;
    align-items: top;
  }

  .bleft {
    display: flex;
    flex-direction: column;
    height: 88vh;
    flex-basis: 25%;
    padding: 10px 10px 0 10px;
  }

  .bcenter {
    flex-basis: 50%;
    padding: 20px 0 0 0px;
  }

  .bright {
    flex-basis: 25%;
    padding: 10px 10px 0 10px;
  }

  .blboxs {
    border-radius: 16px;
    border: 2px solid rgba(10, 67, 158, 1);
    text-align: center;
    padding: 10px;
    /* flex: 1; */
    margin-top: 10px;
    /* height: 33%; */
  }

  .bltgird {
    border: 1px solid rgba(70, 169, 195, 1);
    /* padding: 20px 10px; */
    /* width: 80px;
  height: 80px; */
    display: flex;
    flex-direction: column;
    text-align: center;
    align-items: center;
    justify-content: center;
    padding: 10px 0;
  }

  .gird1 {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 6px;
    margin-top: 10px;
  }

  .gird1title {
    color: #fff;
    font-size: 12px;
    margin-top: 2px;
    font-weight: bold;
    transform: scale(0.8);
    white-space: nowrap;
  }

  .bctopmain {
    display: flex;
  }

  .bctopblock {
    flex-grow: 1;
    text-align: center;
    flex-grow: 1;
    width: 0;
    display: flex;
    flex-direction: column;
  }

  .bccenter {
    border: 1px solid rgba(29, 238, 255, 1);
  }

  .bcbottom {
    display: flex;
    margin-top: 10px;
  }

  .bcbbox {
    flex-grow: 1;
    border: 2px solid rgba(10, 67, 158, 1);
    border-radius: 16px;
    padding: 10px;
    width: 50%;
  }

  .bcbleft {
    margin-right: 10px;
  }

  .brbbox {
    flex-grow: 1;
    border: 2px solid rgba(10, 67, 158, 1);
    border-radius: 16px;
    padding: 10px;
    margin-top: 10px;
  }

  .va-table {
    color: #75f9fd;
    font-size: 8px;
    border-spacing: 0;
    border-collapse: collapse;
    margin: 0;
    padding: 0;
    width: 100%;
    margin-top: 10px;
  }

  .va-table th,
  .va-table td {
    padding: 0.85rem 0rem;
    text-align: center;
    border: 1px solid #ddd;
    font-size: 12px;
  }

  .bctnum {
    font-size: 25px;
    color: #1deeff;
    background: linear-gradient(90deg, rgba(0, 177, 253, 0.73), rgba(0, 178, 178, 0));
    text-align: left;
    padding-left: 30px;
  }

  .bcbleftfor {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 10px;
  }

  .mytag {
    border-radius: 7.5px;
    width: 22px;
    height: 15px;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    margin-right: 5px;
  }

  .bcbtitle {
    color: #fff;
    font-size: 10px;
    white-space: nowrap;
    margin-right: 5px;
    width: 90px;
  }
</style>
