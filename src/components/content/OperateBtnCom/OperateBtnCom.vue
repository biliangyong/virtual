<!--
 * @Author: zhangzhe 437050740@qq.com
 * @Date: 2024-09-22 16:05:32
 * @LastEditors: zhangzhe 437050740@qq.com
 * @LastEditTime: 2024-09-24 17:40:49
 * @FilePath: \marketf:\web\liangda-navigator\src\views\indexPage\components\navigationCom.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
    <div class="operate-com">
        <img class="operate-btn"
            :src="require(`./images/operate-icon${(item.hover || item.showBool) ? (index + 's') : index}.png`)" alt=""
            v-for="(item, index) in operateData" :key="index" @mouseover="item.hover = true;"
            @mouseleave="item.hover = false;" @click="operateBtnClick(item)"
            :class="{ 'extra-spacing': index === 4 }"> <!-- 仅为博物馆按钮添加额外间距 -->
    </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref, defineEmits, defineProps, watch } from "vue";
const props = defineProps({
    data: {
        type: Array,
        default: () => []
    }
});
const operateData = ref([]);
watch(
    () => props.data,
    (newValue) => {
        operateData.value = newValue.map(item => {
            item.showBool = false;
            item.hover = false;
            return item;
        });
    },
	{ immediate: true }
);
const emits = defineEmits(['operateBtnClick'])
onMounted(() => {
});
onUnmounted(() => {
})
function operateBtnClick(itemData) {
    operateData.value.forEach(item => item.showBool = itemData.type == item.type);
    emits('operateBtnClick', itemData);
}
</script>

<style lang="scss">
.operate-com {
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 114px;
    right: 50px;

    .operate-btn {
        width: 78px;
        height: 78px;
        cursor: pointer;
        margin-bottom: 12px; // 默认间距
    }

    .extra-spacing {
        margin-bottom: 36px; // 特殊间距
    }
}
</style>
