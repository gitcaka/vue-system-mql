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
        <img
          style="height: 185px; border: 1px solid #4095e5; border-radius: 5px"
          src="../../../../public/personpic1.png"
        />
        <div style="display: flex; flex-direction: column; width: 100%; padding: 0 20px 0 20px">
          <div style="display: flex; align-items: center; justify-content: space-between; width: 100%">
            <h1 style="font-size: 30px">张权</h1>
            <va-button class="ml-3" color="info" style="border-radius: 5px" :to="{ name: 'label' }"
              >查看完整画像分析</va-button
            >
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
                  <img src="../../../../public/personpic2.png" style="height: 93px" />
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
                    message="根据驾驶员分类给出针对性考核建议"
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
            <img class="chartimg mt-3" src="../../../../public/personpic3.png" style="width: 100%" />
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
              message="根据驾驶员分类给出针对性考核建议"
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

<style>
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
</style>
