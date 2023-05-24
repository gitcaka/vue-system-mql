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
  </div>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  const tabValue = ref(1)

  function tabSwitch(event: any) {
    tabValue.value = event.target.getAttribute('id')
    console.log(tabValue.value)
  }
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
</style>
