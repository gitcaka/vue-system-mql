<template>
  <va-card>
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">关联分析</h1>
    </va-card-title>
    <va-card-content>
      <h1 style="font-size: 12px; font-weight: normal">
        通过大数据技术建立公交驾驶员驾驶行为等数据库， 用实际行为的统计数据得出关联性较强的因素辅助管理
      </h1>
    </va-card-content>
  </va-card>
  <div class="row">
    <div class="flex xl5">
      <va-card>
        <va-card-title style="justify-content: space-between">
          <h1 style="font-size: 20px">典型违规行为组合</h1>
        </va-card-title>
        <va-card-content>
          <div v-for="(item, index) in data1" :key="index" class="grid__container mt-2">
            <p style="width: 20%">{{ item.title1 }}</p>
            <img src="/double_arrow.png" />
            <p style="width: 25%">{{ item.title2 }}</p>
            <p class="ml-3">>></p>
            <p class="ml-3">{{ item.precent }}</p>
            <div class="mr-2" style="margin-left: auto; text-decoration: underline; font-weight: bold">详情</div>
          </div>
        </va-card-content>
      </va-card>
    </div>
    <div class="flex xl7">
      <va-card>
        <va-card-title style="justify-content: space-between">
          <h1 style="font-size: 20px">行为—画像关联性分析</h1>
        </va-card-title>
        <va-card-content>
          <div v-for="(item, index) in data2" :key="index" class="grid__container mt-2">
            <p style="width: 15%">{{ item.title1 }}</p>
            <img src="/arrow3.png" style="height: 12px" />
            <p style="width: 12%">{{ item.title2 }}</p>
            <p class="ml-3">{{ item.precent }}</p>
            <p class="ml-3">{{ item.score }}</p>
            <p class="ml-3">{{ item.variance }}</p>
            <div class="mr-2" style="margin-left: auto; text-decoration: underline; font-weight: bold">详情</div>
          </div>
        </va-card-content>
      </va-card>
    </div>
  </div>
  <div class="row">
    <div class="flex xs6">
      <va-card>
        <va-card-title style="justify-content: space-between">
          <h1 style="font-size: 20px">行为成因分析</h1>
        </va-card-title>
        <va-card-content>
          <div v-for="(item, index) in data3" :key="index" class="grid__container mt-2">
            <p style="width: 15%">{{ item.title1 }}</p>
            <img src="/arrow4.png" style="height: 12px" />
            <p class="ml-3" style="width: 25%">{{ item.title2 }}</p>
            <p class="ml-3">>></p>
            <p class="ml-3">{{ item.precent }}</p>
            <div class="mr-2" style="margin-left: auto; text-decoration: underline; font-weight: bold">详情</div>
          </div>
        </va-card-content>
      </va-card>
    </div>
    <div class="flex xs6">
      <va-card style="height: 100%">
        <va-card-title style="justify-content: space-between">
          <h1 style="font-size: 20px">历届排名走向分析</h1>
        </va-card-title>
        <va-card-content>
          <table class="va-table2">
            <thead>
              <tr>
                <th>降分占比</th>
                <th>违规行为/身体状况</th>
                <th>人数</th>
                <th></th>
              </tr>
            </thead>
            <tbody style="font-weight: bold">
              <tr>
                <td>87.54%</td>
                <td>攻击性行为</td>
                <td>32</td>
                <td style="text-decoration: underline">详情</td>
              </tr>
              <tr>
                <td>64.46%</td>
                <td>疲劳驾驶</td>
                <td>22</td>
                <td style="text-decoration: underline">详情</td>
              </tr>
            </tbody>
          </table>
        </va-card-content>
      </va-card>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  const data1 = ref([
    { title1: '与乘客口角', title2: '攻击性驾驶', precent: '32%' },
    { title1: '急刹过多', title2: '行驶稳定性差', precent: '57%' },
    { title1: '急刹过多', title2: '行驶稳定性差', precent: '57%' },
  ])
  const data2 = ref([
    { title1: '30~35年龄段', title2: '急刹', precent: '占比 >>45%', score: '均分 >> 14.8', variance: '方差 >> 2.4' },
    {
      title1: '35~40年龄段',
      title2: '分心驾驶',
      precent: '占比 >> 32%',
      score: '均分 >> 21.5',
      variance: '方差 >> 1.4 ',
    },
    {
      title1: '25~30年龄段',
      title2: '车距不稳',
      precent: '占比 >> 56%',
      score: '均分 >> 12.3',
      variance: '方差 >> 4.2 ',
    },
  ])
  const data3 = ref([
    { title1: '心率变化大', title2: '速度维稳不平稳', precent: '32%' },
    { title1: '睡眠质量低', title2: '驾驶不平稳', precent: '43%' },
    { title1: '分心驾驶', title2: '车距保持差', precent: '23%' },
  ])
</script>

<style scoped>
  .grid__container {
    min-height: 3rem;
    border-radius: 0.5rem;
    padding: 1rem;
    box-sizing: border-box;
    background-color: #158de3;
    font-size: 14px;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 10px;
    font-weight: bold;
  }

  .va-table2 {
    width: 100%;
    background-color: #158de3;
    border-radius: 10px;
    color: #fff;
    font-size: 14px;
  }

  .va-table2 td,
  th {
    padding: 15px 0;
    border: 1px solid #fff;
    text-align: center;
  }

  /* .va-table2 td {
  } */

  .va-table2 th {
    background-color: #154ec1;
  }
</style>
