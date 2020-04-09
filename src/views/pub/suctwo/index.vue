<template>
    <div id="suctwo">
        <div class="suc_container">
            <div class="wrap" v-for="(item, idx) in suctwos" :key="idx">
                <img :src="item.suctwo_img" :alt="item.suctwo_title">
                <div class="signform">
                    <div class="sign_title">
                        <a href="program.html">{{ item.suctwo_title }}</a>
                    </div>
                    <div class="sign_body">
                        <ul>
                            <li class="sign_time">奖项: {{ item.suctwo_prize }}</li>
                            <li class="match_time">参赛人员: {{ item.suctwo_person }}</li>
                        </ul>
                    </div>
                </div>
                <div class="sign">
                    <a href="" class="sign_btn">详情</a>
                </div>
            </div>
          
          <page-component :total="page.totalSize" :page="page" @pageChange="(item)=>handlePageChange(item)" />
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import PageComponent from '@/components/pagination'
export default {
    components: {
      PageComponent
    },
    data() {
      return {
        page: {
          currentPage: 0, // 当前页
          pageSize: 0, // 每页条数
          totalSize: 0, // 总条数
          totalPage: 0 // 总页数
        },
        suctwos: [
          // {
          //   'suctwo_img': 'http://5b0988e595225.cdn.sohucs.com/images/20180802/e65bffab6d8b41329ce9f1f87c14d6d0.jpeg',
          //   'suctwo_title': '《第一届“中国软件杯”双创大赛》',
          //   'suctwo_person': '张三、李四、王五',
          //   'suctwo_prize': '国家级三等奖'
          // },
          // {
          //   'suctwo_img': 'http://www.52jingsai.com/data/attachment/portal/201510/26/125414syxzqq98hymym9hj.jpg',
          //   'suctwo_title': '《“创青春”四川省大学生创新创业大赛》',
          //   'suctwo_person': '张三、李四、王五',
          //   'suctwo_prize': '四川省级铜奖'
          // },
          // {
          //   'suctwo_img': 'http://www.ahip.cn/UserFiles/Image/152335161059456264.jpg',
          //   'suctwo_title': '第九届蓝桥杯大赛',
          //   'suctwo_person': '张三、李四、王五',
          //   'suctwo_prize': '国家级一等奖'
          // }
        ]
      }
    },
    mounted() {
      this.getSucTwoList()
    },
    methods: {
      handlePageChange(item) {
        axios.get('sub/train/findAllSucTwo?page=' + item.currentPage + '&pageSize=' + item.pageSize).then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.suctwos = res.data.data.list
        })
      },
      getSucTwoList() {
        axios.get('sub/train/findAllSucTwo?page=1&pageSize=10').then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.suctwos = res.data.data.list
          console.log(res.data.data.list)
        })
      }
    }
}
</script>

<style lang="scss">
.suc_container .wrap{
    width: 1000px;
    margin: 10px auto;
    height: 200px;
    display: flex;
    box-shadow: 0 0 8px #ccc;
}

.suc_container .wrap img{
    width: 25%;
}

.suc_container .wrap .signform{
    width: 60%;
    height: 200px;
    padding-left: 20px;
}

.suc_container .wrap .signform .sign_title{
    display: flex;
    margin: 20px 0 10px 0;
}

.suc_container .wrap .signform .sign_title a{
    font-size: 14px;
    font-weight: bold;
    display: block;
    color: #3D3D3D;
}

.suc_container .wrap .signform .sign_title a:hover{
    color: #BE392A;
}

.suc_container .wrap .signform .sign_title span{
    display: block;
    width: 70px;
    height: 20px;
    margin-left: 10px;
    text-align: center;
    border-radius: 3px;
    background-color: orange;
    color: #fff;
}

.suc_container .wrap .signform .sign_body{
    margin: 20px auto;
}

.suc_container .wrap .signform .sign_body ul li{
    min-width: 100px;
    margin: 0 20px 30px 0;
    font-size: 14px;
    color: #000;
    padding-left: 30px;
    background: url('../../../assets/images/suc/icons.png') no-repeat;
}

.suc_container .wrap .signform .sign_body ul li:nth-child(1){
    background-position: 0 -242px;
}

.suc_container .wrap .signform .sign_body ul li:nth-child(2){
    background-position: 0 -280px;
}

.suc_container .wrap .signform .sign_body ul li:nth-child(3){
    background-position: 0 -206px;
}

.suc_container .wrap .signform .sign_body ul li:nth-child(4){
    background-position: 0 -170px;
}
.suc_container .wrap .sign{
    width: 30%;
    height: 200px;
    /*border: 1px solid blue;*/
}

.suc_container .wrap .sign .sign_btn{
    width: 140px;
    height: 40px;
    line-height: 40px;
    display: block;
    border-radius: 20px;
    font-size: 20px;
    margin: 60px 0 0 60px;
    color: #fff;
    background-color: orange;
    text-align: center;
}

.suc_container .wrap .sign .sign_time{
    text-align: center;
    margin: 15px;
}    
</style>