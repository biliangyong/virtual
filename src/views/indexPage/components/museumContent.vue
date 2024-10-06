<!--
 * @Author: zhangzhe 437050740@qq.com
 * @Date: 2024-09-24 13:38:40
 * @LastEditors: zhangzhe 437050740@qq.com
 * @LastEditTime: 2024-09-24 20:07:06
 * @FilePath: \marketf:\web\liangda-navigator\src\views\indexPage\components\museumContent.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
    <div class="museum-content">
        <div class="content-html" style="text-indent: 2em;">
            <p style="margin: 0px;">中国计量大学计量博物馆坐落于学校日月湖北岸，位于求是南楼4至5层。博物馆总建筑面积约为1700平方米，主展厅的建筑面积约1400平方米，内部空间划分为公共活动区、展陈区、文物库房区、办公区等。累计投资1000余万元，收集馆藏文物近1000余件，通过各种实物、文字图片以及多媒体手段的应用，按历史发展时间顺序，集中展现了中国古代计量史和中国近现代计量史，诠释了计量文化的发展脉络和内涵精华，无论展馆定位、内涵还是展品种类、内容都位居全国计量专业博物馆前列。</p>
            <p style="margin: 0px;">计量博物馆由古代度量衡和近现代计量两个展区构成。度量衡是中华民族的古老文明和智慧的结品，数千年深深植根于中华文明和民族的观念习惯中，广泛应用于生产、生活的各个领域，历史悠久，博大精深。四楼展厅是近现代计量部分，从明末清初传教士带来的西方科学导致的中国传统计量的变革谈起，揭示了近现代计量制度及管理的演变，民国时期统一度量衡、建立并推行近代计量制度的努力，时间计量的进展等，展示了新中国计量事业发展的历史进程，对新中国计量机构的演变，计量管理体系的法制化过程，计量教育、计量传播和计量科学研究、当代计量管理体系的特征等做了深入梳理。</p>
        </div>
        <div class="museum-qrcode">
            <img src="../images/museum-qrcode.png" alt="" />
            虚拟博物馆
        </div>
        <img class="museum-experience-btn" src="../images/experience-btn.png" alt="" @click="PageJump('https://www.720yun.com/t/bbvknyf7d7m?scene_id=30075449')" />
    </div>
</template>

<script setup>
import { onMounted, onUnmounted, inject } from "vue";
let PageJump = inject("PageJump");

onMounted(() => {
});
onUnmounted(() => {
})
</script>
<style lang="scss">
.museum-content {
    width: 100%;
    flex: 1;
    padding: 48px;
    padding-top: 24px;
    box-sizing: border-box;
    position: relative;

    .content-html {
        max-height: 30vh;
        overflow: hidden;
        overflow-y: scroll;
        font-family: 'NotoSansHans-Regular';
        font-size: 16px;
        color: #1F4470;
        line-height: 28px;
        letter-spacing: 2px;
    }

    .museum-qrcode {
        display: flex;
        flex-direction: column;
        align-items: center;
        font-weight: bold;
        font-size: 18px;
        font-family: 'NotoSansHans-Regular';
        color: #1F4470;
        line-height: 18px;
        position: absolute;
        left: 66px;
        bottom: 40px;

        img {
            height: 130px;
            width: 130px;
            position: absolute;
            left: -18px;
            bottom: 26px;
        }
    }

    .museum-experience-btn {
        width: 180px;
        height: 48px;
        position: absolute;
        bottom: 100px;
        right: 440px;
        cursor: pointer;
    }
}
</style>