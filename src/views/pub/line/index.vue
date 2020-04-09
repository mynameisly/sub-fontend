<template>
    <div id="line">
        <div class="block">
            <el-timeline>
                <el-timeline-item v-for="(item, idx) in lines" :key="idx" :timestamp="item.line_year" :color="'red'" :size="'large'" placement="top">
                    <el-card>
                        <h2 style="font-size:20px;font-weight:bold">{{ item.line_title }}</h2>
                        <p>{{ item.line_intro }}</p>
                        <div class="imgBox">
                            <img :src="item.line_img">
                        </div>
                    </el-card>
                </el-timeline-item>
            </el-timeline>
        </div>

        <!-- <page-component :total="lines.length" @pageChange="(item)=>handlePageChange(item)" /> -->
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
    name: 'timeLine',
    data() {
        return {
            page: {
              currentPage: 0, // 当前页
              pageSize: 0, // 每页条数
              totalSize: 0, // 总条数
              totalPage: 0 // 总页数
            },
            lines: [
              // {   
              //     'line_year': '2011',
              //     'line_title': '全国软件专业人才设计与开放大赛',
              //     'line_img': 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1581168061023&di=651c61032288d31a59b7a8debccd69be&imgtype=0&src=http%3A%2F%2Fimg.duoziwang.com%2F2016%2F12%2F14%2F14190452742.jpg',
              //     'line_intro': '简 介:计算机实训室成立于200F8年9月，实验室主要承担C语言、java语言编程、数据库开发、网站设计和Android系统等综合课程的增强性训练，同时也承相学科竞赛培训、Android系统等综合课程的增强性训练，同时也承相学科竞赛培训Android系统等综合课程的增强性训练Android系统等综合课roid系统等综合课程的增强性训练' 
              // },
              // {
              //     'line_year': '2012',
              //     'line_title': '第一届中国软件杯大学生软件设计大赛',
              //     'line_img': 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1581168085774&di=a24e6c503497ebd14eb24c6da63428b6&imgtype=0&src=http%3A%2F%2Fhbimg.huabanimg.com%2F2ac5c5c5a341bae3d8eca733f40db910a21daf772106e-4KSfna_fw236',
              //     'line_intro': '简 介:计算机实训室成立于200F8年9月，实验室主要承担C语言、java语言编程、数据库开发、网站设计和Android系统等综合课程的增强性训练，同时也承相学科竞赛培训、Android系统等综合课程的增强性训练，同时也承相学科竞赛培训Android系统等综合课程的增强性训练Androd系统等综合课程的增强性训练Android系统等综合课程的增强性训练' 
              // },
              // {
              //     'line_year': '2013',
              //     'line_title': '第二届中国软件杯大学生软件设计大赛',
              //     'line_img': 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=2987701559,1536179413&fm=15&gp=0.jpg',
              //     'line_intro': '简 介:计算机实训室成立于200F8年9月，实验室主要承担C语言、java语言编程、数据库开发、网站设计和Android系统等综合课程的增强性训练，同时也承相学科竞赛培训、Android系统等综合课程的增强性训练，同时也承相学科竞赛培训Android系统等综合课程的增强性训练Androiid系统等综合课程的增强性训练Android系统等综合课程的增强性训练' 
              // },
              // {
              //     'line_year': '2014',
              //     'line_title': '第五届蓝桥杯复赛',
              //     'line_img': '',
              //     'line_intro': '简 介:计算机实训室成立于200F8年9月，实验室主要承担C语言、java语言编程、数据库开发、网站设计和Android系统等综合课程的增强性训练，同时也承相学科竞赛培训、Android系统等综合课程的增强性训练，同时也承相学科竞赛培训Android系统等综合课程的增强性训练Android系统等综Android系统等综合课程的增强性训练' 
              // },
              // {
              //     'line_year': '2014',
              //     'line_title': '第六届蓝桥杯复赛',
              //     'line_img': '',
              //     'line_intro': '简 介:计算机实训室成立于200F8年9月，实验室主要承担C语言、java语言编程、数据库开发、网站设计和Android系统等综合课程的增强性训练，同时也承相学科竞赛培训、Android系统等综合课程的增强性训练，同时也承相学科竞赛培训Android系统等综合课程的增强性训练Androi程的增强性训练Android系统等综合课程的增强性训练' 
              // },
              // {
              //     'line_year': '2015',
              //     'line_title': '2015年参加第六届蓝桥杯决赛',
              //     'line_img': ''
              // },
              // {
              //     'line_year': '2016',
              //     'line_title': '第二届互联网+大赛',
              //     'line_img': ''
              // }
            ]
        }
    },
    mounted() {
      this.getlineList()
    },
    methods: {
      handlePageChange (item) {
        axios.get('/sub/line/findAllLine?page=' + item.currentPage + '&pageSize=' + item.pageSize).then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.lineList = res.data.data.list
        })
      },
      getlineList () {
        axios.get('/sub/line/findAllLine?page=1&pageSize=10').then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.lines = res.data.data.list
          console.log(res.data.data.list)
        })
      }
    }
}
</script>

<style lang="scss">
.el-timeline {
  padding: 30px 0 0 30px;
}
.el-timeline-item__tail {
  border-left: 2px solid red;
}    
</style>
<style scoped>
.block p {
  padding: 10px 0;
  font-size: 16px;
}
.imgBox {
  display: flex;
  justify-content: space-around;
  /* border:1px solid red; */
}
</style>