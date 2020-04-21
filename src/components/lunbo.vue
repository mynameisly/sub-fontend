<template>
    <div class="carousel">
        <el-carousel trigger="click" height="600px">
            <el-carousel-item v-for="(item, idx) in lunbos" :key="idx">
                <img :src="require('E://FileDown//' + item.photo_name)" style="width: 100%; height: 600px;" :alt="item.photo_img">
            </el-carousel-item>
        </el-carousel>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'lunbo',
    data() {
        return {
            lunbos: [
                // {
                //     'lunbo_name': '轮播图1',
                //     'lunbo_img': 'https://img.zcool.cn/community/01c4635acd6955a8012138679530f7.jpg@1280w_1l_2o_100sh.jpg'
                // },
                // {
                //     'lunbo_name': '轮播图1',
                //     'lunbo_img': 'http://img0.imgtn.bdimg.com/it/u=1475605360,857492036&fm=15&gp=0.jpg'
                // }
            ],
        }
    },
    mounted() {
        this.getlunboList()
    },
    methods: {
        getlunboList () {
            axios.get('/sub/files/findAllFile?page=1&pageSize=10').then((res) => {
                this.lunbos = res.data.data.list
                // console.log('this.lunbos',this.lunbos)
            })
        }
    }
}
</script>