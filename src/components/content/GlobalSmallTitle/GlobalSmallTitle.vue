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
    font-weight: bold;
    font-size: 20px;
    font-family: 'NotoSansHans-Regular';
    color: #1f4470;
    line-height: 24px;

    img {
        width: 1.4vh;
        height: 0.9vh;
        margin-right: 0.4vh;
    }
}
</style>