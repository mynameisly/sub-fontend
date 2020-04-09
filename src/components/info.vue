<template>
    <div class="mtop">
        <div class="mlist">
            <div class="title">
                <a href="/pub/sign">学科竞赛信息</a>
                <a href="/pub/sign" class="more">更多>></a>
            </div>
            <div class="mlistBox">
                <div class="mlist_left" v-for="(item, idx) in infos" :key="idx">
                    <div class="mlist_top">
                        <img :src="item.info_icon" width="62" height="62" />
                    </div>
                    <div class="mlist_title">{{ item.info_title }}</div>
                    <div class="mlist_main">{{ item.info_intro }}</div>
                    <div class="mlist_ah">
                        <span>{{ item.info_state }}</span>
                    </div>
                    <div class="letGo">
                        <a href="/pub/sign">立即查看>></a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Info',
    data() {
        return {
            infos: [
                {
                    'info_icon': '../assets/images/index/idx_info1.png',
                    'info_title': '经典算法竞赛',
                    'info_intro': '经典算法竞赛是在全国高中数学联赛的基础上进行的一次...',
                    'info_state': '火热报名中'
                },
                {
                    'info_icon': '../assets/images/index/idx_info2.png',
                    'info_title': 'ACM 国际大学生程序设计竞赛 ',
                    'info_intro': '中国物理学会重视ACM 国际大学生程序设计竞赛 (ACM/ICPC)....',
                    'info_state': '报名已过'
                },
                {
                    'info_icon': '../assets/images/index/idx_info3.png',
                    'info_title': '微软创新杯全球学生大赛',
                    'info_intro': '微软创新杯全球学生大赛是由国家教育部 微软创新杯全球学生大赛是由国家教育部微软创新杯全球学生大赛是由国',
                    'info_state': '火热报名中'
                }
            ]
        }
    },
    mounted () {
        this.getinfolist()
    },
    methods: {
        getinfolist () {
            axios.get('/sub/subject/findAllSubject?page=1&pageSize=10').then((res) => {
                this.page.currentPage = res.data.data.currentPage
                this.page.pageSize = res.data.data.size
                this.page.totalPage = res.data.data.pages
                this.page.totalSize = res.data.data.total
                this.infos = res.data.data.list
                console.log(res.data.data.list)
            })
        }
    }
}
</script>

<style lang="scss">
    // 学科竞赛信息样式
        .mtop {
            width:100%;
            height:auto;
            overflow:hidden;
            padding:0;
            margin:0 auto;
            background:#FFF;
            position:relative;
        }
        .title {
            width:1000px;
            height:auto;
            padding:0 0 15px;
            margin: 30px auto 20px;
            text-align:center;
            position:relative;
        }
        .title a{
            font-size: 30px;
            color: #000000;
        }
        .title a.more{
            float: right;
            font-size: 18px;
        }

        .title a.more:hover{
            color: orange;
        }
        .mlist {
            width:1000px;
            height:400px;
            overflow:hidden;
            padding:0;
            margin:0 auto;
            position:relative;
        }
        .mlistBox{
            position: relative;
            display: flex;
            justify-content: space-between;
        }
        .mlist_left {
            width: 270px;
            height: 270px;
            overflow: hidden;
            padding-top: 10px;
            margin-right: 3px;
            /* background: url(../images/mb1.jpg) no-repeat left center; */
            border:1px solid gainsboro;
            box-shadow: 1px 1px 10px #888888;
            float: left;
            background-size: 100%;
            position: relative;
            transition: all ease-in .3s;
        }
        .mlist_left:hover{
            box-shadow: 0 10px 20px rgba(0,0,0,.2);
        }
        .mlist_top {
            width:180px;
            height:62px;
            overflow:hidden;
            padding:0;
            margin:0 auto;
            margin-top: 30px;
            text-align:center;
            position:relative;
        }
        .mlist_title {
            width:230px;
            height:30px;
            overflow:hidden;
            line-height:30px;
            padding:0;
            margin: 0 auto;
            text-align:center;
            font-size:14px;
            font-weight:bold;
            color:#3D3D3D;
            position:relative;
        }
        .mlist_main {
            width:220px;
            height:75px;
            overflow:hidden;
            padding:5px 0 0;
            margin:0 auto;
            line-height:180%;
            color:#656565;
            position:relative;
        }
        .mlist_ah {
            height: 30px;
            text-align: center;
            font-size: 16px;
        }
        .letGo{
            width: 110px;
            border-radius: 5px;
            cursor: pointer;
            text-align: center;
            line-height: 36px;
            height: 36px;
            background-color: rgb(231,101,88);
            margin: 0 auto;
        }
        .letGo a{
            font-size: 16px;
            color: #fff;
            font-weight: bold;
        }
</style>