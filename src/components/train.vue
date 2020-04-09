<template>
    <div id="train">
        <div class="title">
            <a @click="toTrain">竞赛培训</a>
            <a @click="toTrain" class="more">更多>></a>
        </div>
        <div class="train_container">
            <ul class="train_container_lf">
                <li v-for="(item, idx) in trains" :key="idx">
                    <a href="#">{{ item.train_content }}</a>
                </li>
            </ul>
            
            <ul class="train_container_rg">
                <li  v-for="(item, idx) in trains" :key="idx">
                    <a href="#">{{ item.train_time }}</a>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Train',
    data () {
      return {
        trains: [
          // {
          //     'train_content': '四川工商学院2019届毕业生毕业纪念册设计、制作招标集训四川工商学院2019届毕业生毕业纪念册设计、制作招标集训制作招标集训',
          //     'train_time': '2019-5-26'
          // },
          // {
          //     'train_content': '大陆架是打开链接发来是利空打击拉萨酱豆腐啦是独立房间',
          //     'train_time': '2019-6-26'
          // },
          // {
          //     'train_content': '四川工商学院2019届毕业生毕业纪念册设计、制作招标集训',
          //     'train_time': '2019-7-26'
          // },
          // {
          //     'train_content': '四川工商学院2019届毕业生毕业纪念册设计、制作招标集训',
          //     'train_time': '2019-8-26'
          // },
          // {
          //     'train_content': '四川工商学院2019届毕业生毕业纪念册设计、制作招标集训',
          //     'train_time': '2019-7-26'
          // },
          // {
          //     'train_content': '四川工商学院2019届毕业生毕业纪念册设计、制作招标集训',
          //     'train_time': '2019-8-26'
          // },
          // {
          //     'train_content': '四川工商学院2019届毕业生毕业纪念册设计、制作招标集训',
          //     'train_time': '2019-7-26'
          // },
          // {
          //     'train_content': '四川工商学院2019届毕业生毕业纪念册设计、制作招标集训',
          //     'train_time': '2019-8-26'
          // }
        ]
      }
    },
    mounted () {
        this.gettrainList()
    },
    methods: {
      toTrain() {
        this.$router.push({path: '/pub/team'})
      },
      gettrainList () {
        axios.get('/sub/train/findAllTrain?page=1&pageSize=10').then((res) => {
          this.trains = res.data.data.list
          console.log('train', res.data.data.list)
        })
      }
    }
}
</script>

<style lang="scss">
.train_container{
    margin-bottom: 40px;
    box-shadow: 0px 1px 2px #000;
    width: 1000px;
    margin: 0 auto 30px;
    display: flex;
    justify-content: space-between;
}
.train_container_lf {
    padding: 20px 0 0 20px;
    width: 88%;
    li {
        padding-bottom: 10px;
        a {
            color: #000;
            width: 90%;
            display: inline-block;
            white-space: nowrap;
            text-overflow: ellipsis;
            overflow: hidden;
        }
        a:hover{
            color: red;
            text-decoration: underline;
        }
    }
}
.train_container_rg {
    padding: 20px 20px 0 0;
    li {
        height: 25px;
        padding-bottom: 10px;
        a {
            color: #000;
            display: inline-block;
        }
        a:hover{
            color: red;
        }
    }
}

</style>