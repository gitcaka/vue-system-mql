<template>
  <va-card>
    <va-card-title style="justify-content: space-between">
      <h1 style="font-size: 20px">关联性分析</h1>
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
          <div class="grid__container" v-for="(item, index) in data1" :key="index">
            {{ item.title1 }}
            <img src="../../../public/double_arrow.png" alt="" />
            <div style="margin-right: 10px">{{ item.title2 }}</div>
            》{{ item.precent }}
            <div style="margin-left: 10px; text-decoration: underline; font-weight: bold">详情</div>
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
          <h1 style="font-size: 12px; font-weight: normal">
            通过大数据技术建立公交驾驶员驾驶行为等数据库， 用实际行为的统计数据得出关联性较强的因素辅助管理
          </h1>
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
</script>

<style>
  .grid__container {
    min-height: 3rem;
    border-radius: 0.5rem;
    padding: 1rem;
    box-sizing: border-box;
    background-color: #014bdedd;
    font-size: 14px;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 10px;
  }
</style>
