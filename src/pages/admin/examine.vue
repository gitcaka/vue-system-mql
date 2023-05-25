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
                <p>报错</p>
              </div>
            </div>
          </div>
        </va-card-content>
      </va-card>
    </div>
  </div>

  <va-card class="mt-3">
    <va-card-content>
      <div style="display: flex; align-items: center; justify-content: space-around">
        <h1 class="ml-2" style="">请依次选择二级标签以查看分析结果</h1>
        <div style="display: flex; align-items: center; justify-content: center">
          <va-select
            v-model="label1Modal"
            class="mr-2"
            text-by="description"
            label="请选择一级标签"
            track-by="id"
            :options="label1Options"
            style="width: 35%"
          />
          <va-select
            v-model="label2Modal"
            class="mr-2"
            text-by="description"
            label="请选择二级标签"
            track-by="id"
            :options="label2Options"
            style="width: 35%"
          />
          <va-input v-model="search1" placeholder="输入关键字查询" clearable>
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>
        </div>
      </div>
    </va-card-content>
  </va-card>

  <va-card class="mt-3">
    <va-card-content>
      <div style="display: flex; font-size: 20px; align-items: center; width: 100%">
        <va-icon name="ion-ios-arrow-back" style="font-size: 20px; margin-right: 5px" />
        <h1 style="font-size: 15px">返回</h1>
        <h1 class="ml-3" style="color: #158de3">重庆南部公交公司2022年第三季度</h1>
      </div>
    </va-card-content>
  </va-card>

  <va-card class="mt-3">
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">数值调整</h1>
    </va-card-title>
    <va-card-content>
      <div v-for="(item, index) in data1" :key="index" class="grid__container mt-2">
        <p style="width: 12%">{{ item.col1 }}</p>
        <p style="width: 10%; font-size: 20px">{{ item.col2 }}</p>
        <img src="../../../../public/arrow4.png" style="height: 12px" />
        <p class="ml-5" style="width: 12%">{{ item.col3 }}</p>
        <p style="width: 10%; font-size: 20px">{{ item.col4 }}</p>
        <div style="margin-left: auto; text-decoration: underline; font-weight: bold; display: flex">
          <div class="mr-5">数据查看</div>
          <div class="mr-5">调整建议</div>
          <div class="mr-5">信息反馈</div>
        </div>
      </div>
    </va-card-content>
    <div style="width: 100%; display: flex">
      <va-button class="mr-3 mb-3" color="info" style="border-radius: 5px; margin-left: auto">查看往期调整</va-button>
    </div>
  </va-card>

  <va-card class="mt-3">
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">周期调整</h1>
    </va-card-title>
    <va-card-content>
      <div v-for="(item, index) in data2" :key="index" class="grid__container mt-2">
        <p style="width: 12%">{{ item.col1 }}</p>
        <p style="width: 10%; font-size: 20px">{{ item.col2 }}</p>
        <img src="../../../../public/arrow4.png" style="height: 12px" />
        <p class="ml-5" style="width: 12%">{{ item.col3 }}</p>
        <p style="width: 10%; font-size: 20px">{{ item.col4 }}</p>
        <div style="margin-left: auto; text-decoration: underline; font-weight: bold; display: flex">
          <div class="mr-5">数据查看</div>
          <div class="mr-5">调整建议</div>
          <div class="mr-5">信息反馈</div>
        </div>
      </div>
    </va-card-content>
    <div style="width: 100%; display: flex">
      <va-button class="mr-3 mb-3" color="info" style="border-radius: 5px; margin-left: auto">查看往期调整</va-button>
    </div>
  </va-card>

  <va-card class="mt-3">
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">方案调整</h1>
    </va-card-title>
    <va-card-content>
      <table class="va-table2">
        <tbody style="font-weight: bold">
          <tr v-for="(item, index) in projectData" :key="index">
            <td>{{ item.title }}</td>
            <td style="text-decoration: underline">在线预览</td>
            <td style="text-decoration: underline">数据查看</td>
            <td style="text-decoration: underline">文件下载</td>
            <td style="text-decoration: underline">信息反馈</td>
          </tr>
        </tbody>
      </table>
    </va-card-content>
    <div style="width: 100%; display: flex">
      <va-button class="mr-3 mb-3" color="info" style="border-radius: 5px; margin-left: auto">查看往期调整</va-button>
    </div>
  </va-card>

  <div class="row">
    <div class="flex xs7">
      <va-card class="">
        <va-card-title style="justify-content: space-between">
          <h1 style="font-size: 20px">参数权重</h1>
        </va-card-title>
      </va-card>
    </div>
    <div class="flex xs5">
      <va-card class="">
        <va-card-title style="justify-content: space-between">
          <h1 style="font-size: 20px">统计学特征分析：车速</h1>
        </va-card-title>
      </va-card>
    </div>
  </div>

  <va-card class="mt-3">
    <va-card-content>
      <div style="display: flex; align-items: center">
        <h1 style="font-size: 20px">特殊状况指标提示</h1>
        <va-select
          v-model="label3Modal"
          class="ml-3"
          text-by="description"
          track-by="id"
          :options="label3Options"
          style="width: 10%"
        />
      </div>
      <table class="va-table3 mt-2">
        <tbody style="font-weight: bold">
          <tr>
            <td>明显变动指标：超速、转弯速度、未靠边进站</td>
          </tr>
          <tr>
            <td>相对偏离指标：未走公交车专用道、快速变道、转弯速度、高速进出站、急停</td>
          </tr>
          <tr>
            <td>特殊分布指标：呼吸稳定</td>
          </tr>
        </tbody>
      </table>
    </va-card-content>
  </va-card>
</template>

<script setup lang="ts">
  import { ref } from 'vue'

  const currentTime = ref(new Date().toLocaleString().split(' ')[0])
  const dayOfWeek = new Intl.DateTimeFormat('zh-CN', { weekday: 'long' }).format(new Date())
  const label1Modal = ref('')
  const label2Modal = ref('')
  const label3Modal = ref('年')

  const search1 = ref('')
  const label1Options = ref([
    { id: 1, description: '驾驶员身体素质' },
    { id: 2, description: '驾驶员行为' },
    { id: 3, description: '驾驶员技能' },
  ])
  const label2Options = ref([
    { id: 1, description: '身体健康' },
    { id: 2, description: '心理健康' },
    { id: 3, description: '错误驾驶' },
    { id: 4, description: '失误驾驶' },
    { id: 5, description: '违规驾驶' },
    { id: 6, description: '车速异常' },
    { id: 7, description: '车距异常' },
    { id: 8, description: '失误驾驶' },
    { id: 9, description: '平稳性异常' },
  ])
  const label3Options = ref([
    { id: 1, description: '年' },
    { id: 2, description: '月' },
    { id: 3, description: '日' },
  ])
  const data1 = ref([
    { col1: '行驶平均速度', col2: '40km/h', col3: '行驶平均速度', col4: '42km/h' },
    { col1: '行驶平均转矩', col2: '2.8m内', col3: '行驶平均转矩', col4: '2.7m内' },
  ])
  const data2 = ref([
    { col1: '分心驾驶测试...', col2: '4次/周', col3: '分心驾驶测试...', col4: '6次/周' },
    { col1: '行驶平均车速... ', col2: '8次/周', col3: '行驶平均车速... ', col4: '12次/周' },
  ])
  const projectData = ref([
    { title: '重庆南部公交公司2022第三季度分心驾驶测试方案调整...             ' },
    { title: '重庆南部公交公司2022第三季度分心驾驶测试方案调整...             ' },
  ])

  function refresh() {
    console.log(111)
  }
</script>

<style>
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

  .va-table2 td {
    text-align: center;
    border: 2px solid #fff;
    padding: 20px 0;
  }

  .va-table3 {
    width: 100%;
    background-color: #158de3;
    color: #fff;
    font-size: 14px;
  }

  .va-table3 td {
    border: 5px solid #fff;
    padding: 20px 20px;
  }
</style>
