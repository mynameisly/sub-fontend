<template>
    <div id="sign">
        <div class="sign_container">
            <div class="wrap" v-for="(item, idx) in signs" :key="idx">
                <img :src="require('E://fileDown//'+item.sign_img)" :alt="item.sign_title">
                <div class="signform">
                    <div class="sign_title">
                        <a href="program.html">{{ item.sign_title }}</a>
                        <span>{{ item.sign_status }}</span>
                    </div>
                    <div class="sign_body">
                        <ul>
                            <li class="sign_time">报名时间: {{ item.sign_stime }} 至 {{ item.sign_etime }}</li>
                            <li class="match_time">比赛时间: {{ item.sign_sm_time }}至 {{ item.sign_em_time }}</li>
                            <li class="users">主办方: {{ item.sign_sponsor }}</li>
                        </ul>
                    </div>
                </div>
                <div class="sign">
                    <a href="program.html" class="sign_btn">点击报名</a>
                    <div class="sign_time">总时长: {{ item.totaltime }}</div>
                </div>
            </div>
        </div>
        <page-component :total="page.totalSize" :page="page" @pageChange="(item)=>handlePageChange(item)" />
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
            remain_time: '', // 通过js脚本来计算
            page: {
              currentPage: 0, // 当前页
              pageSize: 0, // 每页条数
              totalSize: 0, // 总条数
              totalPage: 0 // 总页数
            },
            signs: [
                // {
                //     sign_img: 'http://img4.imgtn.bdimg.com/it/u=2393385984,3451962260&fm=15&gp=0.jpg',
                //     sign_title: '第十一届四川省大学生程序设计',
                //     sign_stime: '2019-05-20 21:00',
                //     sign_etime: '2019-06-07 19:00',
                //     sign_sm_time: '2019-06-07 19:00',
                //     sign_em_time: '2019-06-07 22:00 ',
                //     sign_sponsor: 'nowcoder.com',
                //     total_time: '3小时'
                // },
                // {
                //     sign_img: 'http://img0.imgtn.bdimg.com/it/u=3476218157,4191248777&fm=26&gp=0.jpg',
                //     sign_title: 'ACM 国际大学生程序设计竞赛 (ACM/ICPC)',
                //     sign_stime: '2020-05-20 21:00',
                //     sign_etime: '2020-06-07 19:00',
                //     sign_sm_time: '2020-06-07 19:00',
                //     sign_em_time: '2020-06-07 22:00 ',
                //     sign_sponsor: 'nowcoder.com',
                //     total_time: '2.5小时'
                // },
                // {
                //     sign_img: 'http://img3.imgtn.bdimg.com/it/u=1517991076,608782391&fm=26&gp=0.jpg',
                //     sign_title: '全国蓝桥杯大赛',
                //     sign_stime: '2020-05-20 21:00',
                //     sign_etime: '2020-06-07 19:00',
                //     sign_sm_time: '2020-06-07 19:00',
                //     sign_em_time: '2020-06-07 22:00 ',
                //     sign_sponsor: 'nowcoder.com',
                //     total_time: '2.5小时'
                // },
                // {
                //     sign_img: 'http://img0.imgtn.bdimg.com/it/u=2277358453,1255399337&fm=15&gp=0.jpg',
                //     sign_title: '微软 “创新杯”大赛',
                //     sign_stime: '2020-05-20 21:00',
                //     sign_etime: '2020-06-07 19:00',
                //     sign_sm_time: '2020-06-07 19:00',
                //     sign_em_time: '2020-06-07 22:00 ',
                //     sign_sponsor: 'nowcoder.com',
                //     total_time: '3小时'
                // },
                // {
                //     sign_img: 'http://img1.imgtn.bdimg.com/it/u=840546883,2952402054&fm=26&gp=0.jpg',
                //     sign_title: '经典算法竞赛',
                //     sign_stime: '2020-05-20 21:00',
                //     sign_etime: '2020-06-07 19:00',
                //     sign_sm_time: '2020-06-07 19:00',
                //     sign_em_time: '2020-06-07 22:00 ',
                //     sign_sponsor: 'nowcoder.com',
                //     total_time: '5小时'
                // },
                // {
                //     sign_img: 'http://pic4.zhimg.com/c22a9bb155bae5bfd16b1b69f7d672db_b.png',
                //     sign_title: 'Topcoder比赛',
                //     sign_stime: '2020-05-20 21:00',
                //     sign_etime: '2020-06-07 19:00',
                //     sign_sm_time: '2020-06-07 19:00',
                //     sign_em_time: '2020-06-07 22:00 ',
                //     sign_sponsor: 'nowcoder.com',
                //     total_time: '4小时'
                // }
            ]
        }
    },
    mounted() {
      this.getsignList()
    },
    methods: {
      handlePageChange (item) {
        axios.get('/sub/sign/findAllSign?page=' + item.currentPage + '&pageSize=' + item.pageSize).then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.signs = res.data.data.list
        })
      },
      getsignList () {
        axios.get('/sub/sign/findAllSign?page=1&pageSize=10').then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.signs = this.handleSignData(res.data.data.list)
        //   console.log('this.sign',res.data.data.list)
        })
      },
      handleSignData(data) {
        const temp = data
        temp.forEach(ele => {
            ele.totaltime = this.formatSeconds((new Date(ele.sign_em_time) - new Date(ele.sign_sm_time))/1000) // 秒
        });
        return temp
      },
      formatSeconds(value) {
        var secondTime = parseInt(value);// 秒
        var minuteTime = 0;// 分
        var hourTime = 0;// 小时
        if(secondTime > 60) {//如果秒数大于60，将秒数转换成整数
            //获取分钟，除以60取整数，得到整数分钟
            minuteTime = parseInt(secondTime / 60);
            //获取秒数，秒数取佘，得到整数秒数
            secondTime = parseInt(secondTime % 60);
            //如果分钟大于60，将分钟转换成小时
            if(minuteTime > 60) {
                //获取小时，获取分钟除以60，得到整数小时
                hourTime = parseInt(minuteTime / 60);
                //获取小时后取佘的分，获取分钟除以60取佘的分
                minuteTime = parseInt(minuteTime % 60);
            }
        }
        var result = "" + parseInt(secondTime) + "秒";
        if(minuteTime > 0) {
            result = "" + parseInt(minuteTime) + "分" + result;
        }
        if(hourTime > 0) {
            result = "" + parseInt(hourTime) + "小时" + result;
        }
        return result;
      }
    }
}
</script>

<style lang="scss">
.sign_container{
    min-height: 1040px;
    .wrap{
        width: 1000px;
        margin: 10px auto;
        height: 200px;
        display: flex;
        box-shadow: 0 0 8px #ccc;
        img{
            width: 25%;
        }
        .signform{
            width: 60%;
            height: 200px;
            padding-left: 20px;
            .sign_title{
                display: flex;
                margin: 20px 0 10px 0;
                a{
                    font-size: 14px;
                    font-weight: bold;
                    display: block;
                    color: #3D3D3D;
                }
                span{
                    display: block;
                    width: 90px;
                    height: 20px;
                    line-height: 20px;
                    margin-left: 10px;
                    text-align: center;
                    border-radius: 3px;
                    background-color: orange;
                    color: #fff;
                }
            }
        }
    }
}
.sign_container .wrap .signform .sign_title a:hover{
    color: #BE392A;
}

.sign_container .wrap .signform .sign_body{
    margin: 20px auto;
}

.sign_container .wrap .signform .sign_body ul li{
    min-width: 100px;
    margin: 0 20px 30px 0;
    font-size: 14px;
    color: #000;
    padding-left: 30px;
    background: url('../../../assets/images/suc/icons.png') no-repeat;
}

.sign_container .wrap .signform .sign_body ul li:nth-child(1){
    background-position: 0 -242px;
}

.sign_container .wrap .signform .sign_body ul li:nth-child(2){
    background-position: 0 -280px;
}

.sign_container .wrap .signform .sign_body ul li:nth-child(3){
    background-position: 0 -206px;
}

.sign_container .wrap .signform .sign_body ul li:nth-child(4){
    background-position: 0 -170px;
}
.sign_container .wrap .sign{
    width: 30%;
    height: 200px;
    /*border: 1px solid blue;*/
}

.sign_container .wrap .sign .sign_btn{
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

.sign_container .wrap .sign .sign_time{
    text-align: center;
    margin: 15px;
}
</style>