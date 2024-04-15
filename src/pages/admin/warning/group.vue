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
        <h1 style="font-size: 20px">驾驶员数据总览</h1>
      </va-card-title>
    </va-card>
    <div class="row">
      <div class="flex xs6" style="height: 100%">
        <va-card>
          <va-card-title style="font-size: 18px; color: #154ec1"
            >不同年龄层关于身体健康与平稳性异常的分布
          </va-card-title>
          <va-card-content style="height: 100%">
            <div style="display: flex">
              <div style="display: flex; flex-direction: column; width: 50%">
                <img class="chartimg" src="/grouppic1.png" />
                <div>
                  <p class="mt-3 mb-2" style="font-size: 15px; font-weight: bold">近期身体素质中及以下人数</p>
                  <img class="chartimg" src="/grouppic2.png" />
                </div>
              </div>
              <div style="width: 50%; padding: 0 0 0 10px">
                <p style="line-height: 1.6">
                  --仅有少部分司机为优质身体素质<br />
                  --心肺功能稳定<br />
                  --反应速度快：通过模拟测验及互联网监测，公交车驾驶员的反应速度普遍较快<br />
                  --身体疲劳：身体疲劳加重可能增加交通事故发生率。<br />
                  --心理压力导致疏忽：部分司机无法有效留意道路状况和相互惊讶地运动<br />
                  --体质存在问题：有些公交车驾驶员个别存在一些健康问题
                </p>
              </div>
            </div>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs6" style="height: auto">
        <va-card style="height: 100%">
          <va-card-title style="font-size: 18px; color: #154ec1">近期驾驶行为统计</va-card-title>
          <va-card-content>
            <div style="display: flex">
              <div style="display: flex; flex-direction: column; width: 50%">
                <img class="chartimg" src="/grouppic3.png" />
                <p class="mt-3 mb-2" style="font-size: 15px; font-weight: bold">近期身体素质中及以下人数</p>
                <img class="chartimg" src="/grouppic4.png" />
              </div>
              <div style="width: 50%; padding: 0 0 0 10px">
                <p style="line-height: 1.6">
                  --疲劳驾驶：一些公交车驾驶员每天需要连续工作多个小时，在长时间开车后会产生困倦和昏睡感，从而危及行车安全。<br />
                  --闯红灯：少数公交车驾驶员可能会闯红灯，并在减速时突然刹车。<br />
                  --加速过快：部分公交车驾驶员在起步、加速过程中速度快、急躁<br />
                  --占道行驶：有些公交车驾驶员会挤压进站点；强迫拥挤上客或加速，造成不良流量、拥堵现象。<br />
                  --随意换道：部分公交车驾驶员喜欢随意变更车道或者超车，这样做容易在驾驶过程中增加风险，导致车辆碰撞事件的发生。<br />
                </p>
              </div>
            </div>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row">
      <div class="flex xs6" style="height: auto">
        <va-card style="height: 100%">
          <va-card-title style="font-size: 18px; color: #154ec1">公交驾驶员技能统计 </va-card-title>
          <va-card-content>
            <div style="display: flex">
              <div style="display: flex; flex-direction: column; width: 50%">
                <img class="chartimg" src="/grouppic5.png" />
                <p class="mt-3 mb-2" style="font-size: 15px; font-weight: bold">近期驾驶员技能较差人数</p>
                <img class="chartimg" src="/grouppic6.png" />
              </div>
              <div style="width: 50%; padding: 0 0 0 10px">
                <p style="line-height: 1.6">
                  --频繁变道：有些公交车驾驶员过度频繁地变换车道，极大影响了开车体验。<br />
                  --闯红灯：少数公交车驾驶员可能会闯红灯，并在减速时突然停车。<br />
                  --加速过快：部分公交车驾驶员在起步、加速过程中速度快、急躁<br />
                  --挨个排队上客：部分公交车驾驶员为了抢占市场，挤压进站点；强行上客或加速，造成不良流量、拥挤现象。
                </p>
              </div>
            </div>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs6" style="height: auto">
        <va-card style="height: 100%">
          <va-card-title style="font-size: 18px; color: #154ec1">分析与建议</va-card-title>
          <va-card-content>
            <p style="line-height: 1.5">
              --统计显示，有30%的公交驾驶员存在过度工作的情况，其中疲劳驾驶情况较为普遍，需要引起注意。<br />
              --没有严格按照交通规则行驶的驾驶员比例较高，许多人都存在违章停车、违法超载、闯红灯等违规行为。<br />
              --没有发现明显的酒驾、毒驾等违法行为，但需要保持对此类行为的警惕。<br />
              --55%的驾驶员经常出现车速控制不稳、方向盘控制不准确的问题，需要提升驾驶技巧。<br />
              --转弯时140个/1000驾驶员存在未示意转向灯而直接转向的行为，给其他车辆和行人带来了潜在的风险。<br />
              --加强身体健康管理，在公司内部设立运动场所、宣传健康生活方式等。<br />
              --加强对违规行为的处罚力度，对肆意违反交通规则的驾驶员视情节轻重进行相应的惩罚。<br />
              --进一步提升驾驶员技术，加强驾驶技能培训和以考代训机制的实施。同时，将驾驶员自主学习和实践机会最大化，并注重他们在封闭环境下的综合测试。
            </p>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <va-card>
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
          <va-pagination v-model="activeTable" :visible-pages="10" :pages="99" />
        </div>
      </va-card-content>
    </va-card>
  </div>

  <div v-else class="mt-4">
    <va-card>
      <va-card-title>
        <h1 style="font-size: 20px">车辆数据总览</h1>
      </va-card-title>
    </va-card>
    <div class="row">
      <div class="flex xs6" style="height: auto">
        <va-card style="height: 100%">
          <va-card-title style="font-size: 15px">车辆检修</va-card-title>
          <va-card-content>
            <img class="chartimg" src="/grouppic7.png" />
          </va-card-content>
          <div style="width: 100%; display: flex">
            <va-button class="mr-3" color="info" style="border-radius: 5px; margin-left: auto">更多</va-button>
          </div>
        </va-card>
      </div>
      <div class="flex xs6" style="height: 100%">
        <va-card>
          <va-card-title style="font-size: 15px">车辆故障统计</va-card-title>
          <va-card-content style="display: flex; justify-content: center; flex-direction: column; align-items: center">
            <img class="chartimg" style="width: 70%" src="/grouppic8.png" />
            <div class="table-wrapper mt-3" style="width: 100%">
              <table class="va-table va-table--striped va-table--hoverable" style="width: 100%">
                <thead>
                  <tr>
                    <th>编号</th>
                    <th>车型</th>
                    <th>故障</th>
                    <th>紧急度</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="fault in vehicleFaults" :key="fault.id">
                    <td>{{ fault.id }}</td>
                    <td>{{ fault.type }}</td>
                    <td>{{ fault.content }}</td>
                    <td><va-badge :text="fault.urgency" :color="getFaultColor(fault.urgency)" /></td>
                  </tr>
                </tbody>
              </table>
            </div>
            <div style="width: 100%; justify-content: space-between; display: flex; margin-top: 10px">
              <div style="width: 10%"></div>
              <va-pagination v-model="activeTable2" :visible-pages="5" :pages="99" />
              <va-button class="mr-3" color="info" style="border-radius: 5px">更多</va-button>
            </div>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs7">
        <va-card>
          <va-card-title style="font-size: 15px">车辆运行载客统计</va-card-title>
          <va-card-content>
            <img class="chartimg" src="/grouppic9.png" />
          </va-card-content>
          <div style="width: 100%; display: flex">
            <va-button class="mr-3 mb-3" color="info" style="border-radius: 5px; margin-left: auto">更多</va-button>
          </div>
        </va-card>
      </div>
      <div class="flex xs5">
        <va-card>
          <va-card-title style="font-size: 15px">司机行为--车辆故障关联 </va-card-title>
          <va-card-content>
            <div v-for="(item, index) in data1" :key="index" class="grid__container mt-2">
              <p style="width: 20%">{{ item.title1 }}</p>
              <img src="/double_arrow.png" />
              <p style="width: 25%">{{ item.title2 }}</p>
              <p class="ml-3">》</p>
              <p class="ml-3">{{ item.precent }}</p>
              <div class="mr-2" style="margin-left: auto; text-decoration: underline; font-weight: bold">详情</div>
            </div>
          </va-card-content>
          <div style="width: 100%; display: flex">
            <va-button class="mr-3 mb-3" color="info" style="border-radius: 5px; margin-left: auto">更多</va-button>
          </div>
        </va-card>
      </div>
    </div>
    <va-card class="mt-2">
      <va-card-title style="justify-content: space-between">
        <h1 style="font-size: 20px">车辆总体数据统计</h1>
      </va-card-title>
      <va-card-content>
        <p style="line-height: 1.5">
          --存在个别车辆轮胎磨损、拼接缝隙明显过大等问题，需要加强二手防治和早期预警工作。<br />
          --一些小型公交车造型、门户风格设计不太符合市场需求，可能会影响车队整体形象。<br />
          --车辆空气净化器管理水平还有待提高，部分车辆内部环境舒适性不高。<br />
          --部分车辆轻微电路故障十分常见，有必要对这类问题加以关注。<br />
          --监督管理方面的数据实际上存在着较大偏差，新型智能监测手段尚未完全启用或应用不充分。<br />
          --排放指量呈现周期性振荡波动，不稳定性存在，建议政府购置更高质量的公共汽车，节能环保此消彼长。<br />
          --虽然车检合格率非常高，但公交车安全隐患不能忽略：例如乘客突发心脏病时，没有及时处理的问题仍需进一步加以关注。<br />
          --公共汽车集中运营优势还有待发挥，譬如为乘客提供现代化便民服务等，以舒适度为建设基础；
        </p>
      </va-card-content>
    </va-card>
    <va-card class="mt-3">
      <va-card-title style="justify-content: space-between">
        <h1 style="font-size: 20px">车辆历史数据总览查询</h1>
      </va-card-title>
      <va-card-content>
        <div style="display: flex; align-items: center">
          <va-input v-model="search1" placeholder="请输入驾驶员姓名" clearable>
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>
          <va-button class="ml-3" color="info" style="border-radius: 5px; padding: 0 20px">查询</va-button>
        </div>
        <div class="table-wrapper">
          <table class="va-table va-table--striped va-table--hoverable" style="width: 100%; color: #000">
            <thead>
              <tr>
                <th>序号</th>
                <th>时段</th>
                <th>标题</th>
                <th>修改时间</th>
                <th>备注</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="user in vehicleInfos" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.peroid }}</td>
                <td style="color: #1684fc; text-decoration: underline">{{ user.title }}{{ user.peroid }}</td>
                <td>{{ user.modify }}</td>
                <td>{{ user.notes }}</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div style="width: 100%; justify-content: center; display: flex; margin-top: 20px">
          <va-pagination v-model="activeTable" :visible-pages="10" :pages="99" color="success" />
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
  const activeTable = ref(1)
  const activeTable2 = ref(1)

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

  function getFaultColor(faultNum: number) {
    if (faultNum <= 6) {
      return 'success'
    } else if (faultNum <= 8) {
      return 'warning'
    } else return 'danger'
  }

  const data1 = ref([
    { title1: '与乘客口角', title2: '攻击性驾驶', precent: '32%' },
    { title1: '急刹过多', title2: '行驶稳定性差', precent: '57%' },
    { title1: '急刹过多', title2: '行驶稳定性差', precent: '57%' },
  ])

  const vehicleInfos = ref([
    {
      id: 11,
      peroid: '2022第三季度（2022.7-2022.9）',
      title: '重庆南部公交公司',
      modify: '2023.1.1',
      notes: '',
    },
    {
      id: 12,
      peroid: '2022年 9月',
      title: '重庆南部公交公司',
      modify: '2023.1.1',
      notes: '统一维护日期：9.16',
    },
    {
      id: 13,
      peroid: '2022年 8月',
      title: '重庆南部公交公司',
      modify: '2022.12.1',
      notes: '',
    },
    {
      id: 14,
      peroid: '2022年 7月',
      title: '重庆南部公交公司',
      modify: '2023.1.1',
      notes: '',
    },
    {
      id: 15,
      peroid: '2022第二季度（2022.4-2022.6）',
      title: '重庆南部公交公司',
      modify: '2022.8.1',
      notes: '',
    },
    {
      id: 16,
      peroid: '2022年 6月',
      title: '重庆南部公交公司',
      modify: '2022.8.1',
      notes: '统一维护日期：6.16',
    },
    {
      id: 17,
      peroid: '2022年 5月',
      title: '重庆南部公交公司',
      modify: '2022.8.1',
      notes: '',
    },
    {
      id: 18,
      peroid: '2022年 4月',
      title: '重庆南部公交公司',
      modify: '2022.6.1',
      notes: '',
    },
    {
      id: 19,
      peroid: '2022第一季度（2022.1-2022.3）',
      title: '重庆南部公交公司',
      modify: '2022.4.21',
      notes: '',
    },
    {
      id: 20,
      peroid: '2022年 3月',
      title: '重庆南部公交公司',
      modify: '2022.4.3',
      notes: '统一维护日期：3.20',
    },
  ])

  const vehicleFaults = ref([
    { id: 3445, type: 1, content: '发动机转速异常', urgency: 10 },
    { id: 5673, type: 2, content: '刹车异常', urgency: 8 },
    { id: 7453, type: 1, content: '稳定性异常', urgency: 8 },
    { id: 8543, type: 1, content: '悬挂磨损', urgency: 6 },
    { id: 1248, type: 4, content: '悬挂磨损', urgency: 5 },
    { id: 7340, type: 3, content: '门控故障', urgency: 3 },
  ])
</script>

<style scoped>
  .tab {
    display: flex;
    justify-content: center;
    font-weight: bold;
    border-radius: 5px;
    align-items: center;
    line-height: 30px;
  }

  .active {
    background-color: #154ec1;
    color: #fff;
    font-size: 20px;
  }

  .deactive {
    font-size: 12px;
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

  .grid__container {
    min-height: 3rem;
    border-radius: 0.5rem;
    padding: 1rem;
    box-sizing: border-box;
    background-color: #0736ad;
    font-size: 14px;
    color: #fff;
    display: flex;
    /* justify-content: space-around; */
    align-items: center;
  }
</style>
