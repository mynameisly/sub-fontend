<template>
  <div id="team">
    <div class="warp" style="min-height:1397px">
      <div class="team_container" v-for='(item, idx) in teams' :key="idx">
        <div class="matchLf">
          <img :src="require('E://fileDown//'+item.team_img)" alt="图片">
        </div>
        <div class="matchIntor">
          <div class="teacher">
              <span>指导老师:</span>
              <p>{{ item.team_teacher }}</p>
          </div>
          <div class="student">
              <!-- 团队成员最多显示一行，超过以省略号显示 -->
              <span>团队成员:</span>
              <p>{{ item.team_person }}</p>
          </div>
          <div class="comment">
              <!-- 项目评价最多显示一行，超过以省略号显示 -->
              <span>项目评价:</span>
              <p>{{ item.team_comment }}</p>
          </div>
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
        page: {
          currentPage: 0, // 当前页
          pageSize: 0, // 每页条数
          totalSize: 0, // 总条数
          totalPage: 0 // 总页数
        },
        teams: [
          // {
          //   'team_img': 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1580788896909&di=b004a1f474091d0dac07076a79d00ec8&imgtype=0&src=http%3A%2F%2Fimage2.sina.com.cn%2Fty%2Fg%2Fp%2F2005-11-28%2FU1489P6T12D1906488F44DT20051128222903.jpg',
          //   'team_teacher': '王敏',
          //   'team_person': '吴华明、毛小鹏、何旭东、肖诗、吴华明、毛小鹏、何旭东、肖诗、杜金川、梁海彬、柴慧琪、李瑶、姚宾雪',
          //   'team_comment': '项目开发中学到了一个新技能，或者一个知识点，但是通过写博客会加深巩固自己学习的东西，自己写不出来可能说明你对这个知识点理解的还不够深入。'
          // },
          // {
          //   'team_img': 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1580788838344&di=100531143ffed59e986074afe8cd7509&imgtype=jpg&src=http%3A%2F%2Fimg3.imgtn.bdimg.com%2Fit%2Fu%3D1896605933%2C299901340%26fm%3D214%26gp%3D0.jpg',
          //   'team_teacher': '王邦千',
          //   'team_person': '吴华明、毛小鹏、何旭东、肖诗、杜金川、梁海彬、柴慧琪、李瑶、姚宾雪',
          //   'team_comment': '项目开发中学到了一个新技能，或者一个知识点，但是通过写博客会加深巩固自己学习的东西，自己写不出来可能说明你对这个知识点理解的还不够深入。'
          // },
          // {
          //   'team_img': 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1580788974044&di=d679c4be14b20c4829535421dc7dd987&imgtype=0&src=http%3A%2F%2Fbpic.588ku.com%2Felement_origin_min_pic%2F17%2F09%2F28%2Ffa4f9fda07be3f85abbee4cd84295c98.jpg',
          //   'team_teacher': '王邦千',
          //   'team_person': '吴华明、毛小鹏、何旭东、肖诗、杜金川、梁海彬、柴慧琪、李瑶、姚宾雪',
          //   'team_comment': '项目开发中学到了一个新技能，或者一个知识点，但是通过写博客会加深巩固自己学习的东西，自己写不出来可能说明你对这个知识点理解的还不够深入。'
          // },
          // {
          //   'team_img': 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1580788838344&di=100531143ffed59e986074afe8cd7509&imgtype=jpg&src=http%3A%2F%2Fimg3.imgtn.bdimg.com%2Fit%2Fu%3D1896605933%2C299901340%26fm%3D214%26gp%3D0.jpg',
          //   'team_teacher': '王邦千',
          //   'team_person': '吴华明、毛小鹏、何旭东、肖诗、杜金川、梁海彬、柴慧琪、李瑶、姚宾雪',
          //   'team_comment': '项目开发中学到了一个新技能，或者一个知识点，但是通过写博客会加深巩固自己学习的东西，自己写不出来可能说明你对这个知识点理解的还不够深入。'
          // },
          // {
          //   'team_img': 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1580788974044&di=d679c4be14b20c4829535421dc7dd987&imgtype=0&src=http%3A%2F%2Fbpic.588ku.com%2Felement_origin_min_pic%2F17%2F09%2F28%2Ffa4f9fda07be3f85abbee4cd84295c98.jpg',
          //   'team_teacher': '王邦千',
          //   'team_person': '吴华明、毛小鹏、何旭东、肖诗、杜金川、梁海彬、柴慧琪、李瑶、姚宾雪',
          //   'team_comment': '项目开发中学到了一个新技能，或者一个知识点，项目开发中学到了一个新技能，或者一个知识点，但是通过写博客会加深巩固自己学习的东西，自己写不出来可能说明你对这个知识点理解的还不够深入。但是通过写博客会加深巩固自己学习的东西，自己写不出来可能说明你对这个知识点理解的还不够深入。'
          // }
        ]
      }
    },
    mounted() {
      this.getTeamList()
    },
    methods: {
      handlePageChange(item) {
        axios.get('/sub/team/findAllTeam?page=' + item.currentPage + '&pageSize=' + item.pageSize).then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.teams = res.data.data.list
        })
      },
      getTeamList() {
        axios.get('sub/team/findAllTeam?page=1&pageSize=10').then((res) => {
          this.page.currentPage = res.data.data.currentPage
          this.page.pageSize = res.data.data.size
          this.page.totalPage = res.data.data.pages
          this.page.totalSize = res.data.data.total
          this.teams = res.data.data.list
          // console.log(res.data.data.list)
        })
      }
    }
}
</script>

<style lang="scss">
@import "~@/styles/common.scss";
#team{
  width:100%;
  height:100%;
  overflow-y: scroll;
  overflow-x:hidden;
  @include scrollBar(8px);
}  
.team_container{
    width: 930px;
    margin:10px auto;
    display: flex;
    padding: 20px;
    box-shadow: 0 0 5px grey;
    .matchLf{
        width: 25%;
        background: #F39C11;
        img{
            width: 100%;
            height: 100%;
        }
    }
    .matchIntor{
        width: 75%;
        padding: 10px;
        span{
            font-weight: bold;
        }
        p{
            margin: 10px;
        } 
        .student {
            p {
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
            }
        }
        .comment {
            p {
                overflow: hidden;
                text-overflow: ellipsis;
                display: -webkit-box;
                -webkit-line-clamp: 3; // 超过3行省略号显示，兼容性差
                -webkit-box-orient: vertical;
                
            }
        }
    }
}

</style>