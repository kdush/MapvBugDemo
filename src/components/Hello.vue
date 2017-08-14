<template>
  <div class="hello">
    <!-- 简单的百度地图 -->
    <baidu-map class='bm-view' :scroll-wheel-zoom='true' @ready='handler'>
    </baidu-map>
  </div>
</template>

<script>
import Vue from 'vue'
import BaiduMap from 'vue-baidu-map'
import *as mapv from 'mapv'
import axios from 'axios'

// 引入百度地图并传入ak密匙
Vue.use(BaiduMap, {
  ak: '1XjLLEhZhQNUzd93EjU5nOGQ'
})
export default {
  // 留空 计划存放百度地图类
  BmapObject: {},
  // 留空 计划存放地图实例对象
  mapObj: {},
  data() {
    return {
      // 数据点的数据
      largeList: [
        [
          87.88153173,
          39.70716860135857
        ],
        [
          108.2684158354,
          25.354314
        ],
        [
          112.7061793635,
          37.5315
        ],
        [
          112.633886555,
          28.2816287171757
        ],
        [
          98.128777716606,
          32.8284638
        ],
        [
          109.3,
          39.60313523218775
        ],
        [
          97.445419148716,
          25.6012508613
        ],
        [
          97.6376312,
          29.89424201437
        ]]
    }
  },
  methods: {
    // 地图加载就绪后执行
    handler({ BMap, map }) {
      // 打印BMap对象

      console.log(window.BMap)
      // map是地图实例
      this.mapObj = map
      // Bmap是地图类
      this.BmapObject = BMap

      // 大数据点取自data
      let largeList = this.largeList
      // 数据临时数组
      let data = []
      for (var i = 0; i < largeList.length; i++) {
        data.push({
          geometry: {
            type: 'Point',
            coordinates: largeList[i]
          }
        })
      }
      /**
       * @todo  mapv.DataSet里面this.add 报错this问题?
       */
      // 你懂的
      let dataSet = new mapv.DataSet(data)
      // 配置
      let largePointOption = {
        fillStyle: 'rgba(200, 200, 0, 0.8)',
        bigData: 'Point',
        size: 10,
        draw: 'simple',
        zoom: this.zoom,
        center: this.center
      }
      // 到这就卡住了
      let a = new mapv.baiduMapLayer(map, dataSet, largePointOption)
    }
  },
  mounted() {

  },

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bm-view {
  width: 100%;
  height: 1024px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
