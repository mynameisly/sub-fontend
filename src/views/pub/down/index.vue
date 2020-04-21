<template>
    <div id="down">
        <ul style="min-height:912px">
            <li v-for="(item, idx) in downs" :key="idx" style="padding: 10px 0px 10px 10px;border-bottom: 1px solid #FFA500;">
                <a href="#">
                    <span class="content">{{ item.photo_name }}</span>
                    <button @click="down(item.photo_id,item.photo_name)">点击下载</button>
                </a>
            </li>
        </ul>
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
            downs: [
                // {
                //     'photo_name': '第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料'
                // },
                // {
                //     'photo_name': '第10届四川省程序设计大赛参考资料'
                // },
                // {
                //     'photo_name': '第10届四川省程序设计大赛参考资料'
                // },
                // {
                //     'photo_name': '第十届蓝桥杯大赛全国总决赛参赛作品集'
                // },
                // {
                //     'photo_name': '第10届四川省程序设计大赛参考资料'
                // },
                // {
                //     'photo_name': '第10届四川省程序设计大赛参考资料'
                // },
                // {
                //     'photo_name': '第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料'
                // },
                // {
                //     'photo_name': '第十届蓝桥杯大赛全国总决赛参赛作品集第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料第10届四川省程序设计大赛参考资料'
                // }
            ]
        }
    },
    mounted() {
        this.getDownList()
    },
    methods: {
        handlePageChange (item) {
            axios.get('/sub/files/findAllFile?page=' + item.currentPage + '&pageSize=' + item.pageSize).then((res) => {
            this.page.currentPage = res.data.data.currentPage
            this.page.pageSize = res.data.data.size
            this.page.totalPage = res.data.data.pages
            this.page.totalSize = res.data.data.total
            this.downs = res.data.data.list
            console.log('this.page',this.page)
            })
        },
        getDownList() {
            axios.get('/sub/files/findAllFile?page=1&pageSize=10').then((res) => {
                this.page.currentPage = res.data.data.currentPage
                this.page.pageSize = res.data.data.size
                this.page.totalPage = res.data.data.pages
                this.page.totalSize = res.data.data.total
                this.downs = res.data.data.list
                console.log('downs',res.data.data.list)
            })
        },
        down(photo_id,photo_name) {
            axios.get('/sub/files/findAllFile?fileName=' + photo_id).then((res) => {
            // if(res.data.code === 0) {
                // this.$message({
                //     type: 'info',
                //     message: '文件不存在'
                // })
                // } else if (res.data.code === 9) {
                // this.$message({
                //     type: 'info',
                //     message: '文件已失效'
                // })
                // } else {
                window.location.href = 'http://localhost:18083/files/download?fileName=' + photo_name
                // }
            })
        }
    },
}
</script>

<style lang="scss" scoped>
#down {
    width: 900px;
    margin: 10px auto;
    ul li {
        display: flex;
        justify-content: space-between;
        a {
            color: #000;
            width: 890px;
            display: inline-block;
            .content {
                width:90%;
                display:inline-block;
                white-space: nowrap;
                text-overflow: ellipsis;
                overflow: hidden;
            }
            button{
                
            }
        }
        
    }
}
 
</style>