<template>
    <div class="cartoon-com" @click="showTalkBool = !showTalkBool">
        <div class="talk-style" v-if="showTalkBool" @click.stop>
            导航路线已经出来啦，量量可以带你去呦。
            <img src="./images/scene-anm.png" alt="" @click.stop="sceneAnmClick" />
        </div>
    </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";
const showTalkBool = ref(false);//对话框显隐
const emits = defineEmits(["sceneAnmClick"]);
function sceneAnmClick(){
    showTalkBool.value = false;
    emits("sceneAnmClick");
}
</script>
<style lang="scss">
.cartoon-com {
    width: 346px;
    height: 254px;
    background-image: url("./images/cartoon-icon.png");
    background-size: 100% 100%;
    position: absolute;
    right: 0px;
    bottom: 0px;
    cursor: pointer;

    .talk-style {
        width: 290px;
        height: 134px;
        background-image: url("./images/talk-background.png");
        background-size: 100% 100%;
        position: absolute;
        bottom: 240px;
        right: 240px;
        font-family: 'NotoSansHans-Regular';
        font-size: 16px;
        color: #1F4470;
        line-height: 2.2vh;
        padding: 18px;
        padding-top: 24px;
        padding-bottom: 42px;
        box-sizing: border-box;

        //可能要改
        img {
            width: 76px;
            height: 17px;
            position: absolute;
            bottom: 42px;
            right: 18px;
            cursor: pointer;

        }
    }
}
</style>