<template>
    <div id="header">
      <div class="header">
        <div id="logo"></div>
        <div class="header_right">
            <div class="search_sou">
                <input type="image" name="Submit" src="../../assets/images/index/ss.jpg" value="提交" onclick="chksearch()">
            </div>
            <div class="search_put">
                <input name="SeaStr" type="text" class="search_main" id="SeaStr" value="请输入关键词" onfocus="if (value =='请输入关键词'){value =''}" onblur="if (value ==''){value='请输入关键词'}">
            </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
    name: 'Header',
    data() {
        return {

        }
    }
}
</script>

<style lang="scss">
#header {
    width:100%;
    height:90px;
    overflow:hidden;
    padding:0;
    margin:0 auto;
    background:#33495E;
    position:relative;
}
.header {
    width:1000px;
    margin:0 auto;
}
#logo {
    width:450px;
    height:90px;
    overflow:hidden;
    background: url(../assets/images/index/com_logo.png) no-repeat left center;
    background-size: 100%;
    background-color: rgb(51,73,94);
    float:left;
    position:relative;
}
.header_right {
    width:275px;
    height:60px;
    overflow:hidden;
    padding:30px 0 0 0;
    float:right;
    position:relative;
}
.search_sou {
    width:44px;
    height:30px;
    overflow:hidden;
    float:right;
    position:relative;
}
.search_put {
    width:228px;
    height:28px;
    overflow:hidden;
    border:1px solid #5E7C98;
    float:right;
    position:relative;
}
.search_main {
    width:225px;
    height:28px;
    line-height:28px;
    overflow:hidden;
    padding:0 0 0 3px;
    margin:0 auto;
    color: #FFF;
    background:#33495E;
    border:none;
    position:relative;
}
</style>