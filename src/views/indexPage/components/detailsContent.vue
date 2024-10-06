<template>
    <div class="details-content" v-if="data">
        <NormalSwiperCom :data="data.path" />
        <AudioPlayer :audioUrl="data.audio_url" style="margin:16px 0;" />
        <img class="school-icon" src="../images/school-icon.png" alt="" />
        <img class="panorama-icon" src="../images/panorama-icon.png" alt="" @click="PageJump(data.panoramic)"
            v-if="data.panoramic" />
        <div class="content-html" v-html="data.info" v-if="data.info && htmlBool"></div>
    </div>
</template>

<script setup>
import { onMounted, onUnmounted, defineProps, inject } from "vue";
let PageJump = inject("PageJump");

defineProps({
    data: {
        type: Object,
        default: null
    },
    htmlBool: {
        type: Boolean,
        default: false
    },
});
onMounted(() => {
});
onUnmounted(() => {
})
</script>
<style lang="scss">
.details-content {
    position: relative;
    width: 420px;
    height: 100%;
    overflow: hidden;
    overflow-y: scroll;
    display: flex;
    flex-direction: column;

    .school-icon {
        width: 161px;
        height: 160px;
        position: absolute;
        bottom: 0px;
        left: 0px;
        z-index: -1;
    }

    .panorama-icon {
        width: 34px;
        height: 34px;
        position: absolute;
        top: 6px;
        right: 6px;
        z-index: 1;
        cursor: pointer;
    }
//楼宇等
    .content-html {
        flex: 1;
        overflow: hidden;
        overflow-y: scroll;
        font-family: 'NotoSansHans-Regular';
        font-weight: normal;
        font-size: 16px;
        color: #1F4470;
        line-height: 2.6vh;
    }

}
</style>