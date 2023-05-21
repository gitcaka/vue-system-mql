<template>
  <va-card>
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">驾驶员档案信息</h1>
    </va-card-title>
    <va-card-content>
      <h1 style="font-size: 12px; font-weight: normal">您可以根据姓名、工号等基本信息对驾驶员档案进行查询。</h1>
    </va-card-content>
  </va-card>
  <div class="row mt-2" style="justify-content: space-around">
    <div class="flex">
      <va-card>
        <va-card-content>
          <img src="../../../public/drivers_pic1.png" style="height: 200px" />
        </va-card-content>
      </va-card>
    </div>
    <div class="flex">
      <va-card>
        <va-card-content>
          <img src="../../../public/drivers_pic2.png" style="height: 200px" />
        </va-card-content>
      </va-card>
    </div>
    <div class="flex">
      <va-card>
        <va-card-content>
          <img src="../../../public/drivers_pic3.png" style="height: 200px" />
        </va-card-content>
      </va-card>
    </div>
  </div>

  <va-card>
    <va-card-title>驾驶员数据表</va-card-title>
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
        <va-pagination v-model="activeTable" :visible-pages="10" :pages="99" />
      </div>
    </va-card-content>
  </va-card>
</template>

<script setup lang="ts">
  import { ref } from 'vue'

  const search = ref('')
  const workStatusModal = ref('出勤中')
  const activeTable = ref(1)
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
</script>

<style>
  .va-table th {
    text-align: center;
  }

  .va-table td {
    text-align: center;
  }
</style>
