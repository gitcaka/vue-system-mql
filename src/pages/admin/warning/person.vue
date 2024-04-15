<template>
  <va-card>
    <va-card-content>
      <div class="row">
        <div id="0" class="flex xs6 tab" :class="[tabValue == 0 ? 'active' : 'deactive']" @click="tabSwitch">
          车辆数据监测
        </div>
        <div id="1" class="flex xs6 tab" :class="[tabValue == 1 ? 'active' : 'deactive']" @click="tabSwitch">
          驾驶员数据监测
        </div>
      </div>
    </va-card-content>
  </va-card>

  <div v-if="tabValue == 1" class="mt-4">
    <va-card>
      <va-card-title>
        <h1 style="font-size: 20px">驾驶员个人数据查看</h1>
      </va-card-title>
    </va-card>
    <va-card class="mt-3">
      <va-card-content style="display: flex">
        <img style="height: 185px; border: 1px solid #767c88; border-radius: 5px" src="/personpic1.png" />
        <div style="display: flex; flex-direction: column; width: 100%; padding: 0 20px 0 20px">
          <div style="display: flex; align-items: center; justify-content: space-between; width: 100%">
            <h1 style="font-size: 30px">张权</h1>
            <va-button class="ml-3" color="info" style="border-radius: 5px">查看完整画像分析</va-button>
          </div>
          <div class="mt-3" style="display: flex; width: 100%">
            <div class="xs3 flex">
              <va-card color="primary">
                <va-card-title>
                  <h1 style="font-size: 20px">总评分</h1>
                </va-card-title>
                <va-card-content>
                  <div style="display: flex; justify-content: center">
                    <h1 class="va-h2 ma-0">76分</h1>
                  </div>
                </va-card-content>
              </va-card>
            </div>

            <div class="xs6 flex ml-3 mr-3">
              <va-card color="success" style="height: 100%">
                <va-card-content style="height: 100%; display: flex">
                  <div style="display: flex; flex-direction: column">
                    <h1 style="font-size: 20px">总评分排名</h1>
                    <div class="mt-4" style="display: flex; font-size: 25px">
                      <p>687/1269</p>
                      <p>&nbsp; || &nbsp;</p>
                      <p>占比54.14%</p>
                    </div>
                  </div>
                  <img src="/personpic2.png" style="height: 93px" />
                </va-card-content>
              </va-card>
            </div>

            <div class="xs3 flex">
              <va-card color="info">
                <va-card-title>
                  <h1 style="font-size: 20px">风险指数</h1>
                  <va-popover
                    icon="material-icons-info_outline"
                    color="info"
                    message="分为高、中、低三种"
                    placement="right"
                    open
                  >
                    <va-icon name="material-icons-info_outline" style="margin: 2px 0 0 2px" />
                  </va-popover>
                </va-card-title>
                <va-card-content>
                  <div style="display: flex; justify-content: center">
                    <h1 class="va-h2 ma-0">中</h1>
                  </div>
                </va-card-content>
              </va-card>
            </div>
          </div>
        </div>
      </va-card-content>
    </va-card>
    <div class="row">
      <div class="flex xs5">
        <va-card>
          <va-card-content>
            <div style="display: flex; align-items: center; justify-content: space-between">
              <h1 class="ml-2" style="">近期考核成绩</h1>
              <va-button class="ml-3" color="info" style="border-radius: 5px">详情</va-button>
            </div>
            <img class="chartimg mt-3" src="/personpic3.png" style="width: 100%" />
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs7">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">近期画像分析</h1>
            <va-popover
              icon="material-icons-info_outline"
              color="info"
              message="根据驾驶员的各类信息绘制人物画像，对画像结果进行分析"
              placement="right"
              open
            >
              <va-icon name="material-icons-info_outline" color="info" style="margin: 2px 0 0 2px" />
            </va-popover>
          </va-card-title>
          <va-card-content>
            <p style="color: #767c88">最近更新时间：2023.5.10 星期五</p>
            <table class="va-table va-table--striped va-table--hoverable mt-4" style="width: 100%; color: #000">
              <tbody>
                <tr v-for="(item, index) in imageData" :key="index">
                  <td>{{ item.title }}</td>
                  <td>{{ item.detail }}</td>
                  <td>
                    <va-badge :text="item.rate" :color="getRateColor(item.rate)" />
                  </td>
                </tr>
              </tbody>
            </table>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row">
      <div class="flex xs4">
        <va-card>
          <va-card-title style="justify-content: space-between">
            <h1 style="font-size: 20px">驾驶员健康</h1>
          </va-card-title>
          <va-card-content>
            <div style="display: flex; justify-content: space-between; align-items: center">
              <div style="display: flex; align-items: baseline">
                <h1>评分：</h1>
                <h1 style="color: #e42222; font-size: 28px">49</h1>
              </div>
              <div style="display: flex; align-items: baseline">
                <h1>风险指数：</h1>
                <h1 style="color: #e42222; font-size: 28px">差</h1>
              </div>
            </div>
            <p class="mt-3" style="line-height: 1.75">
              -- 虽然成绩处于中上位置，但是近期 身体素质考核成绩持续下降<br />
              -- <span style="color: #e42222">隐患</span>：缺乏体力无法长时间驾驶<br />
              -- 健康意识<span style="color: #e42222">较差 近期存在睡眠不足的情况</span><br />
              -- 心理访谈<span style="color: #e42222">结果较上次有所下降</span>
            </p>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card>
          <va-card-title style="justify-content: space-between">
            <h1 style="font-size: 20px">驾驶员行为</h1>
          </va-card-title>
          <va-card-content>
            <div style="display: flex; justify-content: space-between; align-items: center">
              <div style="display: flex; align-items: baseline">
                <h1>评分：</h1>
                <h1 style="color: #3d9209; font-size: 28px">96</h1>
              </div>
              <div style="display: flex; align-items: baseline">
                <h1>风险指数：</h1>
                <h1 style="color: #3d9209; font-size: 28px">优</h1>
              </div>
            </div>
            <p class="mt-3" style="line-height: 1.75">
              -- 近期考核持续上升，且仍旧处于 中上位置<br />
              -- <span style="color: #3d9209">改善</span>：本季度攻击性驾驶行为减少<br />
              -- <span style="color: #e42222">隐患</span>：经常超速、闯红灯，增加交 通事故的风险<br />
              -- 相较之前 近期出现<span style="color: #e42222">疲劳驾驶</span>状况
            </p>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card style="height: 100%">
          <va-card-title style="justify-content: space-between">
            <h1 style="font-size: 20px">驾驶员技能</h1>
          </va-card-title>
          <va-card-content>
            <div style="display: flex; justify-content: space-between; align-items: center">
              <div style="display: flex; align-items: baseline">
                <h1>评分：</h1>
                <h1 style="color: #ffd43a; font-size: 28px">84</h1>
              </div>
              <div style="display: flex; align-items: baseline">
                <h1>风险指数：</h1>
                <h1 style="color: #ffd43a; font-size: 28px">中</h1>
              </div>
            </div>
            <p class="mt-3" style="line-height: 1.75">
              -- 近期考核持续上升，且仍旧处于中上位置<br />
              -- <span style="color: #3d9209">改善</span>：急加速峰值相较上季度降低<br />
              -- <span style="color: #e42222">隐患</span>：车辆控制能力差，如刹车、起步时容易出现危险动作
            </p>
          </va-card-content>
        </va-card>
      </div>
    </div>

    <va-card class="mt-3">
      <va-card-title>
        <h1 style="font-size: 20px">驾驶员数据总览</h1>
      </va-card-title>
      <va-card-content>
        <div style="display: flex; align-items: center">
          <va-input v-model="search1" placeholder="请输入驾驶员姓名" clearable style="margin: 10px 10px 10px 0">
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>

          <va-input v-model="search2" placeholder="请输入驾驶员工号" clearable style="margin: 10px 10px 10px 0">
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>

          <div style="display: flex; align-items: center; margin: 10px 10px 10px 0">
            <div style="white-space: nowrap; margin-right: 5px">工作状态:</div>
            <va-select v-model="workStatusModal" text-by="description" track-by="id" :options="workStatusOptions" />
          </div>

          <div style="display: flex; align-items: center">
            <div style="white-space: nowrap; margin-right: 5px">线路:</div>
            <va-select v-model="busLinesModal" text-by="description" track-by="id" :options="busLinesOptions" />
          </div>
        </div>

        <div class="table-wrapper">
          <table class="va-table va-table--striped va-table--hoverable" style="width: 100%; color: #000">
            <thead>
              <tr>
                <th>工号</th>
                <th>姓名</th>
                <th>驾驶车牌号</th>
                <th>驾驶员健康</th>
                <th>驾驶员行为</th>
                <th>驾驶员技能</th>
                <th>预警状态</th>
                <th>数字画像总评分</th>
                <th>实时监测</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="user in driverInfos" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
                <td>{{ user.carNum }}</td>
                <td>
                  <va-badge :text="user.health" :color="getStatusColor(user.health)" />
                </td>
                <td>
                  <va-badge :text="user.behavior" :color="getStatusColor(user.behavior)" />
                </td>
                <td>
                  <va-badge :text="user.skill" :color="getStatusColor(user.skill)" />
                </td>
                <td>
                  <va-badge :text="user.status" :color="getStatusColor(user.status)" />
                </td>
                <td>
                  <va-badge :text="user.score" :color="getScoreColor(user.score)" />
                </td>
                <td style="color: #1684fc; text-decoration: underline">查看</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div style="width: 100%; justify-content: center; display: flex; margin-top: 20px">
          <va-pagination v-model="activeTable1" :visible-pages="10" :pages="99" />
        </div>
      </va-card-content>
    </va-card>
  </div>

  <div v-else class="mt-4">
    <va-card>
      <va-card-title>
        <h1 style="font-size: 20px">车辆数据查看</h1>
      </va-card-title>
    </va-card>
    <div class="row" style="font-weight: bold">
      <div class="flex xs3">
        <va-card color="info">
          <va-card-content>
            <div style="display: flex; justify-content: center">
              <h1 class="va-h4 ma-0">渝D9167D</h1>
            </div>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs3">
        <va-card style="height: 100%">
          <va-card-content style="align-items: center; display: flex; height: 100%; justify-content: center">
            车辆型号：宇通ZK6105H
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs3">
        <va-card style="height: 100%">
          <va-card-content style="align-items: center; display: flex; height: 100%; justify-content: center">
            行驶线路：364
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs3">
        <va-card style="height: 100%">
          <va-card-content style="align-items: center; display: flex; height: 100%; justify-content: center">
            驾驶排班表
            <va-button class="ml-3" color="info" style="border-radius: 5px">查看</va-button>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row">
      <div class="flex xs4">
        <va-card style="height: 100%">
          <va-card-title style="font-size: 15px; justify-content: center">车辆图像</va-card-title>
          <va-card-content>
            <img class="vehcleimg" src="/personpic4.png" />
            <img class="vehcleimg mt-3" src="/personpic5.png" />
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs8">
        <va-card style="height: 100%">
          <va-card-title style="font-size: 15px; justify-content: center">车辆信息</va-card-title>
          <va-card-content>
            <table class="va-table2" style="width: 100%; background-color: #158de3; border-radius: 10px; color: #fff">
              <tbody style="font-weight: bold">
                <tr>
                  <td rowspan="2" style="vertical-align: middle; font-size: 25px">制动</td>
                  <td>制动距离：<span :style="{ color: getColor2('良') }">良</span></td>
                  <td>制动力度：<span :style="{ color: getColor2('优') }">优</span></td>
                  <td>制动稳定性：<span :style="{ color: getColor2('中') }">中</span></td>
                </tr>
                <tr>
                  <td colspan="3">制动距离越短、制动力度越大、制动稳定性越高</td>
                </tr>
              </tbody>
            </table>
            <table
              class="va-table2 mt-3"
              style="width: 100%; background-color: #158de3; border-radius: 10px; color: #fff"
            >
              <tbody style="font-weight: bold">
                <tr>
                  <td rowspan="2" style="vertical-align: middle; font-size: 25px">动力</td>
                  <td>最大功率：<span :style="{ color: getColor2('优') }">优</span></td>
                  <td>最大扭矩：<span :style="{ color: getColor2('差') }">差</span></td>
                  <td>响应性：<span :style="{ color: getColor2('危险') }">危险</span></td>
                </tr>
                <tr>
                  <td colspan="3">制动距离越短、制动力度越大、制动稳定性越高</td>
                </tr>
              </tbody>
            </table>
            <table
              class="va-table2 mt-3"
              style="width: 100%; background-color: #158de3; border-radius: 10px; color: #fff"
            >
              <tbody style="font-weight: bold">
                <tr>
                  <td rowspan="2" style="vertical-align: middle; font-size: 25px">照明</td>
                  <td>照度：<span :style="{ color: getColor2('优') }">优</span></td>
                  <td>均匀度：<span :style="{ color: getColor2('中') }">中</span></td>
                  <td>色温：<span :style="{ color: getColor2('良') }">良</span></td>
                </tr>
                <tr>
                  <td colspan="3">制动距离越短、制动力度越大、制动稳定性越高</td>
                </tr>
              </tbody>
            </table>
            <table
              class="va-table2 mt-3"
              style="width: 100%; background-color: #158de3; border-radius: 10px; color: #fff"
            >
              <tbody style="font-weight: bold">
                <tr>
                  <td rowspan="2" style="vertical-align: middle; font-size: 25px">稳定</td>
                  <td>侧倾角：<span :style="{ color: getColor2('优') }">优</span></td>
                  <td>车身姿态：<span :style="{ color: getColor2('良') }">良</span></td>
                  <td>投柿性能：<span :style="{ color: getColor2('良') }">良</span></td>
                </tr>
                <tr>
                  <td colspan="3">制动距离越短、制动力度越大、制动稳定性越高</td>
                </tr>
              </tbody>
            </table>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <va-card>
      <va-card-title style="justify-content: space-between">
        <h1 style="font-size: 20px">危险参数预警</h1>
      </va-card-title>
      <va-card-content>
        <p style="line-height: 1.5">
          制动系统：制动片磨损度达到85%，<span style="color: #e42222">刹车盘出现裂纹和明显磨损</span
          >，制动距离明显变长，需要立即更换零部件。<br />
          悬挂系统：轮胎间隙不平衡，<span style="color: #e42222">车身左右倾斜</span
          >，需更换悬挂系统零部件，以保证车辆行驶的稳定性和安全。<br />
          轮胎压力：轮胎压力偏低，其中左前轮仅为正常压力的60%，将导致轮胎易于磨损、产生过多热量，并降低行驶平稳性。<br />
          发动机故障：发动机排放黑烟且<span style="color: #ffd43a">噪声较大</span
          >，考虑到该车龄已达10年，建议进行彻底维修，以免影响驾驶者的行车安全和乘客体验。<br />
          燃油系统：
          <span style="color: #e42222">泵失灵和燃油泄漏</span>油，应及时处理以避免火灾和环境污染等事故的发生。<br />
          照明系统：车辆<span style="color: #ffd43a">灯光亮度不足</span
          >，夜间行驶时对行车安全造成影响，应及时更换灯泡或整体更换照明系统。<br />
          电气系统：方向指示器、车灯等<span style="color: #ffd43a">配件存在亮度不足、接触不良等问题</span
          >，需要检查并更换相关部件以确保亮度充足、操作稳定。<br />
          空调系统：空调制冷效果不彰，导致驾驶舱内高温难耐，影响驾驶安全。因此，建议进行空调系统完整性检查和维修。<br />
          吸氧系统：<span style="color: #e42222">吸氧装置透氧碳化严重</span
          >，无法正常起到增加车内氧气浓度的作用，需修理或更换。<br />
          安全带：部分乘客座位安全带不存在或破损，其没有达到安全要求，需更换并加强推广安全意识
        </p>
      </va-card-content>
    </va-card>

    <va-card class="mt-3">
      <va-card-title>
        <h1 style="font-size: 20px">车辆信息查询</h1>
      </va-card-title>
      <va-card-content>
        <div style="display: flex; align-items: center">
          <va-input v-model="search1" placeholder="请输入驾驶员姓名" clearable style="margin: 10px 10px 10px 0">
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>

          <va-input v-model="search2" placeholder="请输入驾驶员工号" clearable style="margin: 10px 10px 10px 0">
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>

          <va-input v-model="search2" placeholder="请输入驾驶员车牌号" clearable style="margin: 10px 10px 10px 0">
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>

          <div style="display: flex; align-items: center">
            <div style="white-space: nowrap; margin-right: 5px">线路:</div>
            <va-select v-model="busLinesModal" text-by="description" track-by="id" :options="busLinesOptions" />
          </div>
        </div>

        <div class="table-wrapper">
          <table class="va-table va-table--striped va-table--hoverable" style="width: 100%; color: #000">
            <thead>
              <tr>
                <th>驾驶车辆编号</th>
                <th>驾驶车牌号</th>
                <th>工号</th>
                <th>姓名</th>
                <th>预警状态</th>
                <th>数字画像总评分</th>
                <th>实时监测</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="user in driverInfos" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.carNum }}</td>
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
                <td>
                  <va-badge :text="user.status" :color="getStatusColor(user.status)" />
                </td>
                <td>
                  <va-badge :text="user.score" :color="getScoreColor(user.score)" />
                </td>
                <td style="color: #1684fc; text-decoration: underline">查看</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div style="width: 100%; justify-content: center; display: flex; margin-top: 20px">
          <va-pagination v-model="activeTable1" :visible-pages="10" :pages="99" />
        </div>
      </va-card-content>
    </va-card>
  </div>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  const tabValue = ref(1)
  const activeTable1 = ref(1)
  const search1 = ref('')
  const search2 = ref('')
  const workStatusModal = ref('出勤中')
  const workStatusOptions = ref([
    { id: 1, description: '出勤中' },
    { id: 2, description: '休息中' },
  ])
  const busLinesModal = ref('201')
  const busLinesOptions = ref([
    { id: 1, description: '201' },
    { id: 2, description: '24' },
    { id: 3, description: '11' },
    { id: 4, description: '6' },
  ])

  function tabSwitch(event: any) {
    tabValue.value = event.target.getAttribute('id')
    console.log(tabValue.value)
  }

  const imageData = ref([
    { title: '疲劳驾驶', detail: '经常没有按规定休息', rate: '不当' },
    { title: '车辆维护', detail: '经常忽略车辆保养和故障处理', rate: '不良' },
    { title: '服务态度', detail: '乘客投诉反馈表明陌生而冷漠', rate: '差' },
    { title: '驾驶技能', detail: '驾驶技术一般，如制动、起步等操作有失误', rate: '一般' },
    { title: '安全意识', detail: '安全意识欠缺，对于路况变化反应过慢', rate: '一般' },
    { title: '违章行为', detail: '飙车、超速等违反交通规则行为频繁发生', rate: '差' },
  ])

  function getRateColor(rate: string) {
    if (['不当', '不良'].includes(rate)) {
      return 'warning'
    } else if (['差'].includes(rate)) {
      return 'danger'
    } else if (['一般'].includes(rate)) {
      return 'info'
    } else return 'success'
  }

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

  function getColor2(str: string) {
    if (['优'].includes(str)) {
      return '#00FF7F'
    } else if (['差', '危险'].includes(str)) {
      return '#d40d52'
    } else if (['中'].includes(str)) {
      return '#FFD43A'
    } else return '#fff'
  }

  const driverInfos = ref([
    {
      id: '0452',
      name: '张权',
      carNum: '渝A9167D',
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
      health: '优',
      behavior: '中',
      skill: '优',
      status: '安全',
      score: '89',
    },
  ])
</script>

<style scoped>
  .active {
    background-color: #154ec1;
    color: #fff;
    font-size: 20px;
  }

  .deactive {
    font-size: 12px;
  }

  .tab {
    display: flex;
    justify-content: center;
    font-weight: bold;
    border-radius: 5px;
    align-items: center;
    line-height: 30px;
  }

  .chartimg {
    background-color: #001a5a;
    width: 100%;
    padding: 30px 0 20px 0;
    border-radius: 10px;
  }

  .va-table th {
    text-align: center;
  }

  .va-table td {
    text-align: center;
  }

  .va-table2 td {
    text-align: center;
    border: 1px solid #fff;
    padding: 15px 0;
  }

  .vehcleimg {
    width: 100%;
    border-radius: 10px;
  }
</style>
