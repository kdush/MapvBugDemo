<template>
  <div class="hello">
    <baidu-map class='bm-view' :scroll-wheel-zoom='true' @ready='handler'>
    </baidu-map>
  </div>
</template>

<script>
import Vue from 'vue'
import BaiduMap from 'vue-baidu-map'
import *as mapv from 'mapv'
import axios from 'axios'
Vue.use(BaiduMap, {
  ak: '1XjLLEhZhQNUzd93EjU5nOGQ'
})
export default {
  BmapObject: {},
  mapObj: {},
  data() {
    return {
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
    handler({ Bmap, map }) {
      this.mapObj = map
      this.BmapObject = Bmap


      let largeList = this.largeList
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
      let dataSet = new mapv.DataSet(data)
      let largePointOption = {
        fillStyle: 'rgba(200, 200, 0, 0.8)',
        bigData: 'Point',
        size: 0.7,
        draw: 'simple',
        zoom: this.zoom,
        center: this.center
      }
      console.log(map)
      let a = new mapv.baiduMapLayer(map, dataSet, largePointOption)
    }
  },
  mounted() {
    console.log(mapv)
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
