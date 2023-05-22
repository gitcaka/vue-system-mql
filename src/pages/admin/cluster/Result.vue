<template>
  <va-card>
    <va-card-title>
      <div style="display: flex; align-items: center">
        <h1 style="font-size: 25px; color: #158de3">结果查看</h1>
        <h1>（驾驶员行车安全聚类分析）</h1>
      </div>
    </va-card-title>
    <va-card-content>
      <h1 style="font-size: 12px; font-weight: normal">基于驾驶员个人信息、驾驶行为等一系列指标进行聚类分析。</h1>
    </va-card-content>
  </va-card>

  <div class="row">
    <div class="flex xs8">
      <va-card>
        <va-card-content>
          <div style="display: flex; align-items: center">
            <h1 class="ml-2" style="">已选择标签</h1>
            <div class="ml-4" style="display: flex; align-items: center; justify-content: center">
              <va-button class="ml-3" color="info" style="border-radius: 5px">身体健康</va-button>
              <va-button class="ml-3" color="info" style="border-radius: 5px">平稳性异常 </va-button>
            </div>
          </div>
        </va-card-content>
      </va-card>
    </div>

    <div class="flex xs4">
      <va-card>
        <va-card-content>
          <va-select
            v-model="labelModal"
            class="ml-2"
            text-by="description"
            track-by="id"
            :options="labelOptions"
            style="width: 65%"
          />
          <va-button class="ml-3" color="info" style="border-radius: 5px" :to="{ name: 'label' }">重新选择</va-button>
        </va-card-content>
      </va-card>
    </div>
  </div>

  <div class="row">
    <div class="flex xs2">
      <va-card style="height: 100%">
        <va-card-title>
          <div style="display: flex; color: rgb(21, 78, 193); align-items: center; font-size: 15px">
            <h1>类别一：</h1>
            <h1 style="">人群画像</h1>
          </div>
        </va-card-title>
        <va-card-content>
          <div style="display: flex; justify-content: center">
            <div class="iconDiv mt-4">
              <va-icon name="material-icons-person" color="success" style="font-size: 100px" />
            </div>
          </div>
        </va-card-content>
      </va-card>
    </div>

    <div class="flex xs10">
      <va-card>
        <va-card-title>
          <div style="display: flex; align-items: center; width: 100%">
            <h1 style="font-size: 20px">特征概述</h1>
            <va-chip shadow class="ml-5" color="success" style="width: 20%">身体健康评分高</va-chip>
            <va-chip shadow class="ml-3" color="success" style="width: 20%">驾驶平稳性优</va-chip>
          </div>
        </va-card-title>
        <va-card-content>
          <h1 style="font-weight: normal; line-height: 1.5">
            根据数据统计，此类驾驶员通常具有如下特征：<br />
            1、身体健康状况良好，没有严重的视力问题或其他身体上的不适。<br />
            2、具有高度的责任心和安全意识，能够保持冷静并迅速应对突发情况。<br />
            3、具备较强的驾驶技能和经验，熟练掌握公交车辆操作技术和相关的法规规定。<br />
            4、有良好的沟通能力和服务意识，注重与乘客的互动交流，并积极解决他们的问题和需求。<br />
            5、对路线和乘客的信息了解充分，能够准确地为乘客提供正确的信息。<br />
            6、注意自我保护和防护，自觉遵守交通安全规则，不轻易超速、闯红灯、穿越非机动车道等行为。<br />
          </h1>
        </va-card-content>
      </va-card>
    </div>
  </div>

  <div class="row">
    <div class="flex xs6" style="height: auto">
      <va-card style="height: 100%">
        <va-card-title style="font-size: 15px">不同年龄层关于身体健康与平稳性异常的分布 </va-card-title>
        <va-card-content> <img class="chartimg" src="../../../../public/resultpic1.png" /> </va-card-content>
      </va-card>
    </div>
    <div class="flex xs6" style="height: 100%">
      <va-card>
        <va-card-title style="font-size: 15px">35~40岁人群关于身体健康与平稳性异常的分布 </va-card-title>
        <va-card-content>
          <img class="chartimg" src="../../../../public/resultpic2.png" />
        </va-card-content>
      </va-card>
    </div>
    <div class="flex xs6">
      <va-card>
        <va-card-title style="font-size: 15px">身体健康异常评价分数数据分布 </va-card-title>
        <va-card-content>
          <img class="chartimg" src="../../../../public/resultpic3.png" />
        </va-card-content>
      </va-card>
    </div>
    <div class="flex xs6">
      <va-card>
        <va-card-title style="font-size: 15px">平稳性异常评价分数数据分布 </va-card-title>
        <va-card-content>
          <img class="chartimg" src="../../../../public/resultpic4.png" />
        </va-card-content>
      </va-card>
    </div>
  </div>
  <va-card>
    <va-card-content>
      <div style="width: 100%; justify-content: center; display: flex">
        <va-pagination v-model="activeTable" :visible-pages="10" :pages="99" />
      </div>
    </va-card-content>
  </va-card>

  <va-card class="mt-4">
    <va-card-title>
      <div style="align-items: center; display: flex">
        <h1 style="font-size: 20px">考核建议</h1>
        <va-popover
          icon="material-icons-info_outline"
          color="info"
          message="根据驾驶员分类给出针对性考核建议"
          placement="right"
          open
        >
          <va-icon name="material-icons-info_outline" color="info" style="margin: 2px 0 0 2px" />
        </va-popover>
      </div>
    </va-card-title>
    <va-card-content>
      <h1 style="font-weight: normal; text-indent: 2em; line-height: 1.5">
        根据聚类结果的分析，我们建议公交车公司在日常管理中针对不同类型的驾驶员，采用差异化的人员培训、管理措施。对于第一类聚集的驾驶员，即身体健康评分高，驾驶平稳性异常评分低，相对慢而平稳的驾驶员，公司可以加强他们的安全意识和驾驶技能方面的培训，以提升整体的安全水平。对于第三类聚集的驾驶员，即身体健康评分中等，驾驶平稳性异常评分高，相对较快且驾驶风格激进的驾驶员，公司需要着重引导其注意安全与文明，倡导平稳驾驶，同时也要算得上是表扬稳定优秀获得好成绩的驾驶员，带动其他驾驶员向他看齐。对于第二类聚集的驾驶员，即身体健康评分和驾驶平稳性异常评分均中等，驾驶风格盛行常规，表现稳健的驾驶员，则需要为其提供合适的阶段性目标计划，以磨炼他们的驾驶技巧，在保证稳健驾驶的前提下，为公交车公司带来更高的运营效益。
      </h1>
    </va-card-content>
  </va-card>
</template>

<script setup lang="ts">
  import { ref } from 'vue'

  const labelModal = ref('类别一')
  const labelOptions = ref([
    { id: 1, description: '类别一' },
    { id: 2, description: '类别二' },
    { id: 3, description: '类别三' },
  ])
  const activeTable = ref(1)
</script>

<style>
  .iconDiv {
    border: #3d9209 5px solid;
    height: 120px;
    width: 120px;
    align-items: center;
    display: flex;
    justify-content: center;
    border-radius: 10px;
  }

  .chartimg {
    background-color: #001a5a;
    width: 100%;
    padding: 30px 0 20px 0;
    border-radius: 10px;
  }
</style>
