<template>
    <div id="home">
        <idx-lunbo/>
        <idx-info/>
        <idx-news/>
        <idx-suc/>
        <idx-train/>
    </div>
</template>

<script>
import IdxLunbo from '@/components/lunbo'
import IdxInfo from '@/components/info'
import IdxNews from '@/components/news'
import IdxSuc from '@/components/suc'
import IdxTrain from '@/components/train'
export default {
    components: {
        IdxLunbo,
        IdxInfo,
        IdxNews,
        IdxSuc,
        IdxTrain
    },
    name: 'Home',
    data() {
        return {
            
        }
    }
}
</script>

<style lang="scss">

</style>