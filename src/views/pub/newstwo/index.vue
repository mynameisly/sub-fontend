<template>
    <div id="newstwo">
        <div class="newstwo_container">
            <el-tabs :tab-position="tabPosition">
                <el-tab-pane label="竞赛新闻">
                  <ul style="min-height:511px">
                    <li v-for="(item, idx) in newstwos" :key="idx" style="padding: 15px 0 15px 0;">
                      <a href="#">
                        <span class="content">{{ item.newstwo_content }}</span>
                        <span class="date">{{ item.newstwo_time }}</span>
                      </a>
                    </li>
                  </ul>
                  <page-component :total="page1.totalSize" :page="page1" @pageChange="(item)=>handlePageChange1(item)" />
                </el-tab-pane>
                <el-tab-pane label="通知公告">
                  <ul style="min-height:511px">
                    <li v-for="(item, idx) in notices" :key="idx" style="padding: 15px 0 15px 0;">
                      <a href="#">
                        <span class="content">{{ item.notice_content }}</span>
                        <span class="date">{{ item.notice_time }}</span>
                      </a>
                    </li>
                  </ul>
                  <page-component :total="page2.totalSize" :page="page2" @pageChange="(item)=>handlePageChange2(item)" />
                </el-tab-pane>
            </el-tabs>
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
        tabPosition: 'left',
        page1: { // 竞赛新闻
          currentPage: 0, // 当前页
          pageSize: 0, // 每页条数
          totalSize: 0, // 总条数
          totalPage: 0 // 总页数
        },
        page2: { // 通知公告
          currentPage: 0, // 当前页
          pageSize: 0, // 每页条数
          totalSize: 0, // 总条数
          totalPage: 0 // 总页数
        },
        newstwos: [
          // {
          //   newstwo_content: '第十届蓝桥杯大赛全国总决赛颁奖典礼在北京大学圆满落幕',
          //   newstwo_time: '2018-12-12'
          // },
          // {
          //   newstwo_content: '蓝桥携手百度举办AI技术全国高校巡讲，带领学生走进AI世界蓝桥携手百度举办AI技术全国高校巡讲，带领学生走进AI世界',
          //   newstwo_time: '2018-12-12'
          // },
          // {
          //   newstwo_content: '第十届蓝桥杯大赛规模再创新高',
          //   newstwo_time: '2019-03-29'
          // },
          // {
          //   newstwo_content: '第十届蓝桥杯大赛全国总决赛颁奖典礼在北京大学圆满落幕',
          //   newstwo_time: '2019-06-10'
          // },
          // {
          //   newstwo_content: '【媒体报道】蓝桥杯大赛正式登陆美国 海外分赛即将开启',
          //   newstwo_time: '2018-12-12'
          // },
          // {
          //   newstwo_content: '蓝桥杯国际赛高手云集 中外强强对抗蓄势待发',
          //   newstwo_time: '2018-12-12'
          // },
          // {
          //   newstwo_content: '蓝桥杯大赛暑期教师培训会在贵阳举行',
          //   newstwo_time: '2018-12-12'
          // },
          // {
          //   newstwo_content: '蓝桥杯国际赛高手云集 中外强强对抗蓄势待发',
          //   newstwo_time: '2018-12-12'
          // },
          // {
          //   newstwo_content: '蓝桥携手百度举办AI技术全国高校巡讲，带领学生走进AI世界',
          //   newstwo_time: '2018-12-12'
          // },
          // {
          //   newstwo_content: '第十届蓝桥杯大赛规模再创新高',
          //   newstwo_time: '2018-12-12'
          // }
        ],
        notices: [
          // {
          //   'notice_content': '关于2019年第三届蓝桥杯德国国赛的通知',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '第十届蓝桥杯青少年编程大赛全国总决赛获奖名单',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '蓝桥杯暑期教师集训会（电子类）的通知(更新)',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '第十届蓝桥杯大赛总决赛个人赛获奖名单',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '第十届蓝桥杯青少年编程大赛国际邀请赛获邀名单',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '第十届蓝桥杯青少年编程大赛全国总决赛获奖名单',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '关于2019年第三届蓝桥杯德国国赛的通知',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '关于2019年第三届蓝桥杯德国国赛的通知',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '关于2019年第三届蓝桥杯德国国赛的通知',
          //   'notice_time': '2019-05-31'
          // },
          // {
          //   'notice_content': '关于2019年第三届蓝桥杯德国国赛的通知关于2019年第三届蓝桥杯德国国赛的通知9年第三届蓝桥杯德国国赛的通知',
          //   'notice_time': '2019-05-31'
          // }
        ]
      }
    },
    mounted() {
      this.getNewsTwoList()
      this.getNoticeList()
    },
    methods: {
      handlePageChange1(item) {
        axios.get('/sub/newTwo/findAllNewsTwo?page=' + item.currentPage + '&pageSize=' + item.pageSize).then((res) => {
          this.page1.currentPage = res.data.data.currentPage
          this.page1.pageSize = res.data.data.size//条数
          this.page1.totalPage = res.data.data.pages//总页数
          this.page1.totalSize = res.data.data.total//总共条数
          this.newstwos = res.data.data.list
          // console.log('分页数据',res.data.data.list)
          // console.log('res',res)
          // console.log('item',item)
        })
      },
      getNewsTwoList() {
        axios.get('/sub/newTwo/findAllNewsTwo?page=1&pageSize=10').then((res) => {
          this.page1.currentPage = res.data.data.currentPage
          this.page1.pageSize = res.data.data.size
          this.page1.totalPage = res.data.data.pages
          this.page1.totalSize = res.data.data.total
          this.newstwos = res.data.data.list
          console.log('this.newstwos',res.data.data.list)
        })
      },
      handlePageChange2(item) {
        axios.get('/sub/notice/findAllNotice?page=' + item.currentPage + '&pageSize=' + item.pageSize).then((res) => {
          this.page2.currentPage = res.data.data.currentPage
          this.page2.pageSize = res.data.data.size
          this.page2.totalPage = res.data.data.pages
          this.page2.totalSize = res.data.data.total
          this.notices = res.data.data.list
        })
      },
      getNoticeList() {
        axios.get('/sub/notice/findAllNotice?page=1&pageSize=10').then((res) => {
          this.page2.currentPage = res.data.data.currentPage
          this.page2.pageSize = res.data.data.size
          this.page2.totalPage = res.data.data.pages
          this.page2.totalSize = res.data.data.total
          this.notices = res.data.data.list
        })
      },
    }
}
</script>

<style lang="scss" scoped>
.newstwo_container {
    margin: 10px auto;
    width: 1000px;
    display: flex;
    justify-content: space-between;
    .el-tabs__nav .is-left {
        font-size: 16px;
        height: 45px;
        padding-top: 7px;
        color: #000;
        text-align: center;
    }
    .el-tabs__active-bar{
        height: 45px;
        background: #FFA500;
    }
    .el-tabs__content {
        width: 885px;
        ul li {
            border-bottom: 1px solid #FFA500;
            margin-right: 10px;
            a {
                display: flex;
                justify-content: start;
                color: #000;
                .content {
                    width: 770px;
                    white-space: nowrap;
                    overflow: hidden;
                    text-overflow: ellipsis;
                } 
            }
            
        }
    }
}
</style>