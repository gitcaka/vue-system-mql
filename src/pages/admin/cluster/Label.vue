<template>
  <va-card>
    <va-card-title>
      <div style="display: flex; align-items: center">
        <h1 style="font-size: 25px; color: #158de3">聚类分析</h1>
        <h1>（驾驶员行车安全）</h1>
      </div>
    </va-card-title>
    <va-card-content>
      <h1 style="font-size: 15px; font-weight: normal; line-height: 1.5">
        基于驾驶员个人信息、驾驶行为等一系列指标进行聚类分析。<br />
        请在下栏选择需要进行聚类的属性，以得到相应的分析结果。
      </h1>
    </va-card-content>
  </va-card>

  <va-card class="mt-4">
    <va-card-content>
      <div style="display: flex; align-items: center; justify-content: space-around">
        <h1 class="ml-2" style="">请选择2-3个标签以查看分析结果</h1>
        <div style="display: flex; align-items: center; justify-content: center">
          <va-select
            v-model="label1Modal"
            class="mr-2"
            text-by="description"
            label="label1"
            track-by="id"
            :options="label1Options"
            style="width: 25%"
          />
          <va-select
            v-model="label2Modal"
            class="mr-2"
            text-by="description"
            label="label2"
            track-by="id"
            :options="label2Options"
            style="width: 25%"
          />
          <va-select
            v-model="label3Modal"
            text-by="description"
            label="label3"
            track-by="id"
            :options="label3Options"
            style="width: 25%"
          />
          <va-button class="ml-3" color="info" style="border-radius: 5px" @click="showResult">分析</va-button>
        </div>
      </div>
    </va-card-content>
  </va-card>

  <div class="row mt-2" style="height: 100%">
    <div class="flex xs6" style="height: 100%">
      <va-card>
        <va-card-title style="justify-content: space-between">
          <h1 style="color: rgb(21, 78, 193)">气泡图</h1>
        </va-card-title>
        <va-card-content style="height: 450px">
          <va-chart v-show="ifShowResult" :data="bubbleChartDataGenerated" type="bubble" />
        </va-card-content>
      </va-card>
    </div>

    <div class="flex xs6">
      <va-card>
        <va-card-content>
          <div class="row mt-1" style="font-size: 20px">
            <va-icon name="material-icons-person" color="success" style="font-size: 30px" />
            <p>类别一</p>
          </div>
          <div v-show="ifShowResult" class="mt-3" style="align-items: center; display: flex; width: 100%">
            <va-chip shadow class="mr-2" color="success" style="width: 43%; padding: 5px 0">身体健康评分高</va-chip>
            <va-chip shadow class="mr-2" color="success" style="width: 43%; padding: 5px 0">驾驶平稳性优</va-chip>
            <va-button
              size="small"
              preset="outline"
              border-color="danger"
              color="danger"
              style="border-radius: 5px"
              :to="{ name: 'result' }"
              >详情</va-button
            >
          </div>
        </va-card-content>
      </va-card>

      <va-card class="mt-3">
        <va-card-content>
          <div class="row mt-1" style="font-size: 20px">
            <va-icon name="material-icons-person" color="warning" style="font-size: 30px" />
            <p>类别二</p>
          </div>
          <div v-show="ifShowResult" class="mt-3" style="align-items: center; display: flex; width: 100%">
            <va-chip shadow class="mr-2" color="warning" style="width: 43%; padding: 5px 0">身体健康评分中等</va-chip>
            <va-chip shadow class="mr-2" color="warning" style="width: 43%; padding: 5px 0">驾驶平稳性良</va-chip>
            <va-button
              size="small"
              preset="outline"
              border-color="warning"
              color="warning"
              style="border-radius: 5px"
              :to="{ name: 'result' }"
              >详情</va-button
            >
          </div>
        </va-card-content>
      </va-card>

      <va-card class="mt-3">
        <va-card-content>
          <div class="row mt-1" style="font-size: 20px">
            <va-icon name="material-icons-person" color="danger" style="font-size: 30px" />
            <p>类别三</p>
          </div>
          <div v-show="ifShowResult" class="mt-3" style="align-items: center; display: flex; width: 100%">
            <va-chip shadow class="mr-2" color="danger" style="width: 43%; padding: 5px 0">身体健康评分差</va-chip>
            <va-chip shadow class="mr-2" color="danger" style="width: 43%; padding: 5px 0">驾驶平稳性差</va-chip>
            <va-button
              size="small"
              preset="outline"
              border-color="danger"
              color="danger"
              style="border-radius: 5px"
              :to="{ name: 'result' }"
              >详情</va-button
            >
          </div>
        </va-card-content>
      </va-card>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import { useChartData } from '../../../data/charts/composables/useChartData'
  import { mybubleChartData } from '../../../data/charts'
  import VaChart from '../../../components/va-charts/VaChart.vue'

  const ifShowResult = ref(false)
  const label1Modal = ref('')
  const label2Modal = ref('')
  const label3Modal = ref('')
  const label1Options = ref([
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
  const bubbleChartDataGenerated = useChartData(mybubleChartData, 0.9)

  function showResult() {
    ifShowResult.value = true
  }
</script>
