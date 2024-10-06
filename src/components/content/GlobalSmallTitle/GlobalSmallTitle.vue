<template>
    <div class="global-small-title">
        <img src="./images/title-icon.png" alt="" />
        {{ title }}
    </div>
</template>

<script setup>
import { onMounted, onUnmounted, defineProps } from "vue";
defineProps({
    title: {
        type: String,
        default: "标题"
    },
});
onMounted(() => {
});
onUnmounted(() => {
})
</script>
<style lang="scss">
.global-small-title {
    font-family: 'NotoSansHans-Regular';
    font-weight: bold;
    font-size: 24px;
    color: #1f4470;
    line-height: 20px;

    img {
        width: 17px;
        height: 11px;
        //margin-right: 0.4vh;
    }
}
</style>