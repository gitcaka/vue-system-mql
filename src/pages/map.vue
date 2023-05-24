<template>
  <baidu-map
    :center="{ lng: 106.554988, lat: 29.56598 }"
    :zoom="zoom"
    :scroll-wheel-zoom="true"
    :map-click="false"
    style="width: 100%; height: 100vh"
    @ready="mapReadyHandler"
  >
    <bm-marker
      v-for="item in markers"
      :key="item.id"
      :position="{ lng: item.location[0], lat: item.location[1] }"
      :icon="{ url: item.icon, size: { width: 64, height: 64 } }"
      @click="clickMarker(item)"
    >
    </bm-marker>
    <bm-info-window :show="infoShow" :position="infoPosition" @open="infoWindowOpen" @close="infoWindowClose"
      >{{ infoContent }}
    </bm-info-window>
    <!-- <bm-traffic> </bm-traffic> -->
    <bm-geolocation anchor="BMAP_ANCHOR_BOTTOM_RIGHT" :show-address-bar="false" :auto-location="true"></bm-geolocation>
  </baidu-map>
</template>

<script setup lang="ts">
  import { onMounted, ref } from 'vue'
  const zoom = ref(13)
  const infoShow = ref(false)
  const infoContent = ref('')
  const infoPosition = ref()
  const infoWindowOpen = ref(function () {
    infoShow.value = true
  })
  const infoWindowClose = ref(function () {
    infoShow.value = false
  })

  const mapReadyHandler = ({ Bmap, map }: any) => {
    let mapStyle = { style: 'bluish' }
    map.setMapStyle(mapStyle)
  }

  const markers = ref([
    {
      id: 0,
      location: [106.540205, 29.557017],
      content: '第一个点',
      icon: 'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_yellow.png?sign=54aa5c90eb7d799fc33b36fe70e5172f&t=1684866019',
    },
  ])

  const clickMarker = ref(function (item: { location: any[]; content: string }) {
    infoPosition.value = { lng: item.location[0], lat: item.location[1] }
    infoContent.value = item.content
    infoShow.value = true
  })

  onMounted(() => {
    let createMarks = []
    for (let index = 0; index < 20; index++) {
      let id = index + 1
      let lng = Math.random() * 0.4 + 106.35
      let lat = Math.random() * 0.18 + 29.48
      let content = '第' + id + '个点，经度：' + lng + '；纬度：' + lat
      let icon =
        'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_green.png?sign=720a70f0b04c3267ae886ea8204e26db&t=1684865993'
      let m = Math.random()
      if (m < 0.7) {
        icon =
          'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_green.png?sign=720a70f0b04c3267ae886ea8204e26db&t=1684865993'
      } else if (m < 0.93) {
        icon =
          'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_yellow.png?sign=54aa5c90eb7d799fc33b36fe70e5172f&t=1684866019'
      } else
        icon =
          'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_red.png?sign=c27cad03ad11e27346af83fa20368de0&t=1684865731'
      let mark = { id: id, location: [lng, lat], content: content, icon: icon }
      createMarks.push(mark)
    }

    for (let index = 0; index < 30; index++) {
      let id = index + 1
      let lng = Math.random() * 0.15 + 106.45
      let lat = Math.random() * 0.06 + 29.53
      let content = '第' + id + '个点，经度：' + lng + '；纬度：' + lat
      let icon =
        'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_green.png?sign=720a70f0b04c3267ae886ea8204e26db&t=1684865993'
      let m = Math.random()
      if (m < 0.7) {
        icon =
          'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_green.png?sign=720a70f0b04c3267ae886ea8204e26db&t=1684865993'
      } else if (m < 0.93) {
        icon =
          'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_yellow.png?sign=54aa5c90eb7d799fc33b36fe70e5172f&t=1684866019'
      } else
        icon =
          'https://6361-caka-5gj3lc4k180a451d-1308169089.tcb.qcloud.la/point_red.png?sign=c27cad03ad11e27346af83fa20368de0&t=1684865731'
      let mark = { id: id, location: [lng, lat], content: content, icon: icon }
      createMarks.push(mark)
    }
    markers.value = createMarks
  })
</script>
