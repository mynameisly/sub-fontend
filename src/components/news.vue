<template>
    <div id="camp">
        <div class="camp">
            <div class="title">
            <a href="/pub/newstwo">竞赛新闻</a>
            <a href="/pub/newstwo" class="more">更多>></a>
            </div>
            <div class="camp">
                <div class="camp_list" v-for="(item, idx) in news" :key="idx">
                <div class="camp_top"><a href="/pub/newstwo"><img :src="item.news_img" width="300" height="165" /></a></div>
                <div class="camp_title"><a href="/pub/newstwo">{{ item.news_title }} </a></div>
                <div class="teacher_main">{{ item.news_intro }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'News',
    data() {
        return {
            news: [
                {
                    'news_img': '',
                    'news_title': 'ACM 国际大学生程序设计竞赛',
                    'news_intro': '本届国际大学生程序设计竞赛吸引了近5万名来自全球六大洲的110个国家和地区、共计3233所高校的选手报名参赛。最终来自全球47个国家和地区的135支团队脱颖而出晋级世界总决赛，其中复旦大学、南京大学、清华大学、北京大学、浙江大学、东北大学等17所中国大陆高校参赛。'
                },
                {
                    'news_img': '',
                    'news_title': '蓝桥杯大赛',
                    'news_intro': '蓝桥杯大赛作为目前的专业IT赛事，其社会影响力和专业认可度逐年扩大，为给不同国家的学生提供更开放融合的竞赛平台，促进国内外专业和文化交流，蓝桥杯大赛首次走出国门增设国际赛，致力于为全世界的优秀专业学生互通有无，提供一个相互了解、交流和切磋的机会。首届蓝桥杯国际赛将于2017年10月在美国开赛，目前正在火热报名中。'
                },
                {
                    'news_img': '',
                    'news_title': '微软 “创新杯”大赛',
                    'news_intro': '“创新杯”四届大赛累计覆盖全省80余所高校，近3万名选手参赛，收集作品近8000件，10余项在全国总决赛中荣获佳绩。本次大赛从2018年10月启动，为期6个月，有主赛和专项赛两个赛道。主赛道主要面向我省高校学生，分为科技创新组和应用创业组；专项赛道面向全社会征集优秀项目，分为人工智能组、大数据组、区块链组和AR/VR组等。大赛设置了一二三等奖、组织奖、导师奖、专项赛奖等奖项。'
                }
            ]
        }
    }
}
</script>

<style lang="scss">
#camp {
	width:100%;
	height:auto;
	overflow:hidden;
	padding:5px 0 30px;
	margin:0 auto;
	background:#F39C11;
	border-top:1px solid #FFF;
	position:relative;
}
.camp {
	width:1000px;
	height:auto;
	overflow:hidden;
	padding:0;
	margin:0 auto;
	position:relative;
}
.camp_list {
	width:320px;
	height:420px;
	overflow:hidden;
	background: #FFF;
	margin-right:13px;
	float:left;
	position:relative;
}
.camp_list1 {
	width:320px;
	height:420px;
	overflow:hidden;
	background: #FFF;
	float:right;
	position:relative;
}

.camp_list .teacher_main,
.camp_list1 .teacher_main{
    font-size: 14px;
	padding: 10px;
}

.camp_top {
	width:300px;
	height:165px;
	overflow:hidden;
	padding:0;
	margin:10px auto 0;
	text-align:center;
	position:relative;
}
.camp_title {
	width:300px;
	height:30px;
	overflow:hidden;
	line-height:30px;
	padding:10px 0 0;
	margin:0 auto;
	color:#323232;
	font-size:14px;
	font-weight:bold;
	position:relative;
}
.camp_title a:active,.camp_title a:link,.camp_title a:visited {
	color:#3E3E3E;
	font-size:14px;
	font-weight:bold;
}
.camp_title a:hover {
	color:#F00;
	text-decoration:underline
}
   
</style>