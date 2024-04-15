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
    <va-card class="mt-3">
      <va-card-content style="display: flex; align-items: flex-end">
        <div style="text-align: center">
          <img style="height: 185px; border: 1px solid #767c88; border-radius: 5px" src="/personpic1.png" />
          <h1 class="mt-1" style="font-size: 30px">张权</h1>
        </div>
        <div style="display: flex; width: 100%">
          <div class="xs6" style="display: flex; flex-direction: column; align-items: center; width: 50%">
            <va-chip class="mb-2" shadow color="success" style="">监控视角</va-chip>
            <video src="/video1.mp4" autoplay muted loop style="width: 80%; border-radius: 5px"></video>
          </div>
          <div class="xs6" style="display: flex; flex-direction: column; align-items: center; width: 50%">
            <va-chip class="mb-2" shadow color="success" style="">第一视角</va-chip>
            <video src="/video2.mp4" autoplay muted loop style="width: 80%; border-radius: 5px"></video>
          </div>
        </div>
      </va-card-content>
    </va-card>

    <div class="row">
      <div class="flex xs8">
        <va-card>
          <va-card-title>
            <h1 style="font-size: 20px">驾驶员行为监测</h1>
          </va-card-title>
          <va-card-content>
            <va-chip
              v-for="(item, index) in behaviorLabels"
              :key="index"
              shadow
              color="info"
              style="margin: 0 10px 10px 10px; width: 21%"
            >
              {{ item.content }}
              <va-icon class="ml-2" name="entypo-record" :style="{ color: item.color }"
            /></va-chip>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card color="info" style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 25px">体温</h1>
          </va-card-title>
          <va-card-content>
            <div style="display: flex; justify-content: space-around; align-items: center">
              <h1 class="va-h1 ma-0" style="color: #00ff7f">36.7 ℃</h1>
              <h1 style="line-height: 2; font-size: 20px">
                --正常范围<br />
                --建议保暖
              </h1>
            </div>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row">
      <div class="flex xs5">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">预警提示</h1>
          </va-card-title>
          <va-card-content>
            <p style="line-height: 2">
              --驾驶员<span style="color: #e42222; font-weight: bold">心率不平稳</span>，疑似处于<span
                style="color: #e42222; font-weight: bold"
                >慌张状态</span
              ><br />
              --驾驶员一度出现<span style="color: #e42222; font-weight: bold">疲劳</span>征兆，注意预防
            </p>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs3">
        <va-card color="info" style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">心率</h1>
          </va-card-title>
          <va-card-content>
            <div style="display: flex; justify-content: space-between; align-items: center">
              <h1 style="line-height: 2; font-size: 15px">
                --平稳<br />
                --正常范围
              </h1>
              <h1 style="color: #00ff7f; font-size: 80px">78</h1>
            </div>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card color="info" style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">血压</h1>
          </va-card-title>
          <va-card-content>
            <div style="display: flex; justify-content: space-between; align-items: center; margin-top: 10%">
              <h1 style="line-height: 2; font-size: 15px">
                --平稳<br />
                --正常范围
              </h1>
              <div style="display: flex; align-items: baseline">
                <h1 style="color: #00ff7f; font-size: 50px">120/80</h1>
                <p class="ml-2" style="font-size: 20px">mmHg</p>
              </div>
            </div>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row">
      <div class="flex xs5">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">精神状态</h1>
          </va-card-title>
          <va-card-content>
            <p style="line-height: 1.75">
              --工作时态度和情绪暴躁、缺乏耐心，时常进行 不必要且消极的抱怨。<br />
              --长时间工作后<span style="color: #e42222; font-weight: bold">疲劳度较高</span>，出现注意力不集中
              的情况，可能会对驾驶安全造成影响。
            </p>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs7">
        <va-card>
          <va-card-title>
            <h1 style="font-size: 20px">近期健康报告简略</h1>
          </va-card-title>
          <va-card-content>
            <p style="line-height: 1.75">
              -- 距上次考核下降12名<br />
              -- 隐患：近期血压血脂相较与过去几次较高，注意身体管理<br />
              -- <span style="color: #e42222; font-weight: bold">健康意识较差</span> 近期存在睡眠不足的情况<br />
              -- 心理访谈结果较上次有所下降<br />
              --无明显疾病特征
            </p>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row mt-2" style="justify-content: center">
      <va-button color="primary" style="border-radius: 5px; padding: 3px 30px">该驾驶员近期数据查看 </va-button>
    </div>
    <va-card class="mt-4">
      <va-card-title>
        <h1 style="font-size: 20px">驾驶员信息查询</h1>
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
  <div v-else class="mt-4">
    <div class="row">
      <div class="flex xs5">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">车辆仪表信息监控</h1>
          </va-card-title>
          <va-card-content>
            <table class="va-table2">
              <tbody style="font-weight: bold">
                <tr>
                  <td>速度表</td>
                  <td>45KM/H</td>
                  <td>转速表</td>
                  <td>1456rpm</td>
                </tr>
                <tr>
                  <td>油量表</td>
                  <td>6L</td>
                  <td>温度表</td>
                  <td>35℃</td>
                </tr>
                <tr>
                  <td>电池电压表</td>
                  <td>220V</td>
                  <td>灯光指示灯</td>
                  <td>正常/开启</td>
                </tr>
                <tr>
                  <td>雨刮指示灯</td>
                  <td>正常/启动</td>
                  <td>制动指示灯</td>
                  <td><span style="color: #e42222; font-weight: bold">损坏</span></td>
                </tr>
                <tr>
                  <td>安全带指示灯</td>
                  <td>正常</td>
                  <td>总里程表</td>
                  <td>2563KM</td>
                </tr>
                <tr>
                  <td>行驶距离表</td>
                  <td>123KM</td>
                  <td>下一站指示器</td>
                  <td>正常</td>
                </tr>
                <tr>
                  <td>声音提示器</td>
                  <td><span style="color: #e42222; font-weight: bold">损坏</span></td>
                  <td>GPS导航系统</td>
                  <td>正常/未开启</td>
                </tr>
                <tr>
                  <td>车载广播系统</td>
                  <td>正常/运作</td>
                  <td>空调温度计</td>
                  <td>正常</td>
                </tr>
                <tr>
                  <td>车门指示灯</td>
                  <td>正常/关闭</td>
                  <td>车窗指示灯</td>
                  <td>正常</td>
                </tr>
              </tbody>
            </table>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs3">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">车辆信息</h1>
          </va-card-title>
          <va-card-content>
            <table class="va-table2">
              <tbody style="font-weight: bold">
                <tr>
                  <td>车辆编号</td>
                  <td>242445468</td>
                </tr>
                <tr>
                  <td>发动机类型</td>
                  <td>汽油发动机</td>
                </tr>
                <tr>
                  <td>车辆型号</td>
                  <td>BDHI12</td>
                </tr>
                <tr>
                  <td>排量</td>
                  <td>10.0L</td>
                </tr>
                <tr>
                  <td>行驶线路</td>
                  <td>364号</td>
                </tr>
                <tr>
                  <td>重量</td>
                  <td>15吨</td>
                </tr>
                <tr>
                  <td>车辆年限</td>
                  <td>12</td>
                </tr>
                <tr>
                  <td>变速器类型</td>
                  <td>手动挡</td>
                </tr>
              </tbody>
            </table>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">车辆数据信息</h1>
          </va-card-title>
          <va-card-content>
            <table class="va-table2">
              <thead>
                <tr>
                  <th>指标</th>
                  <th>状态</th>
                  <th>预警值</th>
                </tr>
              </thead>
              <tbody style="font-weight: bold">
                <tr>
                  <td>车速</td>
                  <td>36 km/h</td>
                  <td>50 km/h</td>
                </tr>
                <tr>
                  <td>碰撞</td>
                  <td colspan="2">正常</td>
                </tr>
                <tr>
                  <td>平稳</td>
                  <td colspan="2">正常</td>
                </tr>
                <tr>
                  <td>线路</td>
                  <td colspan="2">12</td>
                </tr>
                <tr>
                  <td>转速</td>
                  <td colspan="2">1800 rpm</td>
                </tr>
                <tr>
                  <td>冷却液温度</td>
                  <td colspan="2">80 ℃</td>
                </tr>
                <tr>
                  <td>离合器状态</td>
                  <td colspan="2">预警</td>
                </tr>
                <tr>
                  <td>制动器状态</td>
                  <td colspan="2">正常</td>
                </tr>
              </tbody>
            </table>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row">
      <div class="flex xs2">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">违规行为汇报</h1>
          </va-card-title>
          <va-card-content>
            <h1 style="line-height: 1.75; color: #e42222">
              --停车距离过境<br />
              --跟车过近
            </h1>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs2">
        <va-card style="height: 100%">
          <va-card-title>
            <h1 style="font-size: 20px">预警提示</h1>
          </va-card-title>
          <va-card-content>
            <h1 style="line-height: 1.75; color: #e42222">--油量低，请及时添加</h1>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card>
          <va-card-title>
            <h1 style="font-size: 20px">第一视角</h1>
          </va-card-title>
          <va-card-content>
            <video src="/video1.mp4" autoplay muted loop style="width: 100%; border-radius: 5px"></video>
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card>
          <va-card-title>
            <h1 style="font-size: 20px">监控视角</h1>
          </va-card-title>
          <va-card-content>
            <video src="/video2.mp4" autoplay muted loop style="width: 100%; border-radius: 5px"></video>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="row">
      <div class="flex xs4">
        <va-card>
          <va-card-title>
            <h1 style="font-size: 20px">行驶速度曲线</h1>
          </va-card-title>
          <va-card-content>
            <img class="chartimg" src="/realtimepic1.png" />
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card>
          <va-card-title>
            <h1 style="font-size: 20px">行驶加速度曲线</h1>
          </va-card-title>
          <va-card-content>
            <img class="chartimg" src="/realtimepic2.png" />
          </va-card-content>
        </va-card>
      </div>
      <div class="flex xs4">
        <va-card>
          <va-card-title>
            <h1 style="font-size: 20px">车辆颠簸状态</h1>
          </va-card-title>
          <va-card-content>
            <img class="chartimg" src="/realtimepic3.png" />
          </va-card-content>
        </va-card>
      </div>
    </div>
    <va-card>
      <va-card-title style="justify-content: space-between">
        <h1 style="font-size: 20px">综合维护建议</h1>
      </va-card-title>
      <va-card-content>
        <p style="line-height: 1.5">
          机油更换：定期更换机油和机滤可以保证发动机正常运转和延长使用寿命，通常每隔5000至10000公里更换一次。<br />
          刹车系统检查：刹车系统是车辆行驶中的重要保障，需要保持清洁和升级加强，同时定期检查制动片磨损、制动器油管裂纹等情况。<br />
          轮胎保养：轮胎是车辆行驶中承受着很大压力的部件，平均每行驶8000公里需要做一次轮胎旋转变换，同时需要定期测量胎压并进行调整。<br />
          发动机保养：按时更换气滤器和其他细节的调整，可以杜绝发动机颤动、减小空燃比等对发动机的危害，提高其稳定性能。<br />
          汽车电器检查：需要定期检查汽车的电路线路是否老化或插头接口松脱等情况，以避免电器问题成为车辆发生事故的存在因素之一。<br />
          安全气囊应急设置：安全气囊可以起到有效的保护人员的效果，在车辆启动时确保气囊安装完好，达到超速撞击可自动弹出的状态。<br />
          空调保养：由于循环制冷装置会引入外部污染物，车辆内部空气质量需要定期更换滤清器，以保障车内空气流通的安全和健康。
        </p>
      </va-card-content>
    </va-card>
    <va-card class="mt-3">
      <va-card-title>
        <h1 style="font-size: 20px">车辆信息查询</h1>
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

          <va-input v-model="search2" placeholder="请输入驾驶员车牌号" clearable style="margin: 10px 10px 10px 0">
            <template #prependInner>
              <va-icon class="icon-left input-icon" name="search" />
            </template>
          </va-input>

          <div style="display: flex; align-items: center">
            <div style="white-space: nowrap; margin-right: 5px">线路:</div>
            <va-select v-model="busLinesModal" text-by="description" track-by="id" :options="busLinesOptions" />
          </div>
        </div>

        <div class="table-wrapper">
          <table class="va-table va-table--striped va-table--hoverable" style="width: 100%; color: #000">
            <thead>
              <tr>
                <th>驾驶车辆编号</th>
                <th>驾驶车牌号</th>
                <th>工号</th>
                <th>姓名</th>
                <th>预警状态</th>
                <th>数字画像总评分</th>
                <th>实时监测</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="user in driverInfos" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.carNum }}</td>
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
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
  const behaviorLabels = ref([
    { content: '车距保持', color: '#00ff7f' },
    { content: '未系安全带', color: '#FFD43A' },
    { content: '疲劳驾驶', color: '#00ff7f' },
    { content: '转弯半径', color: '#d40d52' },
    { content: '车速维持', color: '#00ff7f' },
    { content: '离开方向盘', color: '#FFD43A' },
    { content: '分心驾驶', color: '#00ff7f' },
    { content: '进站操作', color: '#FFD43A' },
    { content: '驾驶平稳', color: '#00ff7f' },
    { content: '离开驾驶位', color: '#d40d52' },
    { content: '攻击性行为', color: '#FFD43A' },
    { content: '设备控制', color: '#00ff7f' },
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
</script>

<style scoped>
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

  .va-table th {
    text-align: center;
  }

  .va-table td {
    text-align: center;
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
    border: 1px solid #fff;
    padding: 7px 0;
  }

  .va-table2 th {
    text-align: center;
    border: 1px solid #fff;
    padding: 7px 0;
    background-color: #154ec1;
  }

  .chartimg {
    background-color: #001a5a;
    width: 100%;
    padding: 10px 0;
    border-radius: 10px;
  }
</style>
