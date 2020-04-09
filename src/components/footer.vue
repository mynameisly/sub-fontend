<template>
    <div id="footer">
        <div class="footer_bottom" align="center">Copyright © 2019 四川工商学院计算机学院科研综合信息网站</div>
    </div>
</template>

<script>
export default {
    name: 'Footer',
    data() {
        return {

        }
    }
}
</script>

<style lang="scss">
#footer {
    width:100%;
    height:auto;
    overflow:hidden;
    padding:15px 0 10px;
    background:#33495E;
}

.footer_bottom {
    width:1000px;
    height:auto;
    overflow:hidden;
    padding:10px 0;
    margin:0 auto;
    line-height:200%;
    font-size:14px;
    color:#A8B0C7;
    position:relative;
}
.footer_bottom a:active, .footer_bottom a:link, .footer_bottom a:visited {
    font-size:14px;
    color:#A8B0C7
}
.footer_bottom a:hover {
    color:#F00;
}   
</style>