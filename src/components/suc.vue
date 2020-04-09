<template>
    <div id="suc">
        <div class="suc">
            <div class="title">
                <a href="/pub/suctwo">学科竞赛信息</a>
                <a href="/pub/suctwo" class="more">更多>></a>
            </div>
            <div class="sucBox">
                <el-carousel :interval="400000" type="card" height="400px">
                  <el-carousel-item v-for="(item, idx) in sucs" :key="idx">
                      <!-- <h3 class="medium">{{ item }}</h3> -->
                      <video :src="item.suc_video" width="675" height="310" controls="controls"></video>
                      <p>{{ item.suc_title }}</p>
                  </el-carousel-item>
                </el-carousel>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Suc',
    data() {
      return {
        sucs: [
          // {
          //   'suc_video': 'images/video/earth1.25M.mp4',
          //   'suc_title': '第三届全国高校互联网金融应用创新大赛'
          // },
          // {
          //   'suc_video': 'images/video/earth1.25M.mp4',
          //   'suc_title': '“互联网＋”大学生创新创业大赛'
          // },
          // {
          //   'suc_video': 'images/video/earth1.25M.mp4',
          //   'suc_title': 'ACM 国际大学生程序设计竞赛'
          // },
          // {
          //   'suc_video': 'images/video/earth1.25M.mp4',
          //   'suc_title': '“互联网＋”大学生创新创业大赛'
          // },
          // {
          //   'suc_video': 'images/video/earth1.25M.mp4',
          //   'suc_title': '微软 “创新杯”大赛'
          // },
          // {
          //   'suc_video': 'images/video/earth1.25M.mp4',
          //   'suc_title': '蓝桥杯大赛'
          // }
        ]
      }
    },
    mounted () {
      this.getSucList()
    },
    methods: {
      getSucList () {
        axios.get('sub/suc/findAllSuc?page=1&pageSize=5').then((res) => {
          this.sucs = res.data.data.list
        console.log('suc',res.data.data.list)
      })
    }
  }
}
</script>

<style lang="scss">
.el-carousel__item {
    // width: 38.5%;
}
.el-carousel__item--card {
    box-shadow: 0 2px 5px #ddd;
    background: #F39C11;
}
</style>