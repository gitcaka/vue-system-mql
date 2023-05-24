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
        <div style="width: 13%">
          <img
            style="width: 100%; border: 1px solid #4095e5; border-radius: 5px"
            src="../../../../public/personpic1.png"
            alt=""
          />
        </div>
        <div style="display: flex; flex-direction: column; width: 100%; padding: 0 20px 0 20px">
          <div style="display: flex; align-items: center; justify-content: space-between; width: 100%">
            <h1 style="font-size: 30px">张权</h1>
            <va-button class="ml-3" color="info" style="border-radius: 5px" :to="{ name: 'label' }"
              >查看完整画像分析</va-button
            >
          </div>
          <div style="display: flex; width: 100%">
            <div class="xs3 flex">
              <va-card color="success">
                <va-card-title>
                  <h1 style="font-size: 20px">总评分</h1>
                </va-card-title>
                <va-card-content>
                  <div style="display: flex; justify-content: end">
                    <h1 class="va-h2 ma-0 mr-3">76分</h1>
                  </div>
                </va-card-content>
              </va-card>
            </div>

            <div class="xs6 flex">
              <va-card>
                <va-card-title>
                  <h1 style="font-size: 20px">总评分排名</h1>
                </va-card-title>
                <va-card-content> 76分 </va-card-content>
              </va-card>
            </div>

            <div class="xs3 flex">
              <va-card>
                <va-card-title>
                  <h1 style="font-size: 20px">风险指数</h1>
                </va-card-title>
                <va-card-content> 中 </va-card-content>
              </va-card>
            </div>
          </div>
        </div>
      </va-card-content>
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
