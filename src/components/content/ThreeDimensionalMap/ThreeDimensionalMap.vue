<template>
  <div class="dimensional-map">
    <iframe id="iframe" :src="unityUrl" frameborder="0" v-if="unityUrl"></iframe>
  </div>
</template>

<script setup>
import bus from '@/utils/bus.js'
import io from "socket.io-client";
import CryptoJS from 'crypto-js';
import { onMounted, ref, defineProps, defineExpose } from "vue";

const props = defineProps({
  socketUrlValue: { //socket链接地址
    type: String,
    default: "ws://vunity.xuanyantech.com:9801/web",
  },
  keyValue: { //key
    type: String,
    //default: "110073444a3206dcc219cc9355dfafc5",
    default: "969b0caa2bccde1a81905ab6d8c8a93e",
  },
  secretKeyValue: { //密钥
    type: String,
    //default: "f4b8a678acdb585bb516df02270de35f",
    default: "892f55927b6b394f781cc02f836e5210",
  }
});

const socket = ref(null);
const unityUrl = ref(null);
onMounted(() => {
  if (props.socketUrlValue && props.keyValue && props.secretKeyValue)
    start(props.socketUrlValue, props.keyValue, props.secretKeyValue);
});
function start(socketUrl, key, secret) {
  const timestamp = Date.now();
  //生成签名
  const signature = CryptoJS.MD5(`${key}&${secret}&${timestamp}`).toString();
  socket.value = io(`${socketUrl}?key=${key}&timestamp=${timestamp}&sign=${signature}`, { transports: ["websocket"] });

  //连接成功回调
  socket.value.on("connect", function () {
    console.log(`connected`);
    //获取unityWeb链接
    emitStart();
  });

  //断线回调
  socket.value.on("disconnect", function () {
    console.log("disconnected");
  });

  //连接失败回调
  socket.value.on("error", function () {
    console.log("error");
  });

  //场景初始化完成事件
  socket.value.on("sceneLoadComplete", () => {
    console.log("场景初始化完成事件");
    bus.emit("sceneLoadComplete");
  });

  //发送所有点位数据
  socket.value.on("scenePointsComplete", (data) => {
    var pointGroup = JSON.parse(data);
    console.log("接受场景中的点位数据",pointGroup);
  });
  
  //监听标签点击
  socket.value.on("pointClickComplete", (data) => {
    const pointData = JSON.parse(data);
    callAction("switchPointView", pointData.index_code);//切换点位视角
  });
  //监听点位视角到达
  socket.value.on("pointViewComplete", (data) => {
    const pointData = JSON.parse(data);
    bus.emit("pointClickComplete", pointData);
  });
}

function emitStart() {
  callAction("execute", "", (data) => {
    data = JSON.parse(data);
    console.log(data);
    if (data.success) {
      unityUrl.value = data.data.url;
      console.log("Join room success");
    } else {
      console.log("Join room fail");
    }
  });
}

//触发事件 (事件名称,传入参数（类型为字符类型）)
function callAction(action, data = "", fun = null) {
  console.log(`当前事件名称:${action},当前参数:${JSON.stringify()},调用时间:${getTime()}`);
  socket.value?.emit(action, data, function (rspData) {
    console.log(`事件调用成功回调${action} 回调参数:${rspData} 回调时间:${getTime()}`);
    fun?.(rspData);
  });
}

function addZero(x, n) {
  if (x.toString().length < n) {
    x = "0" + x;
  }
  return x;
}

function getTime() {
  var d = new Date();
  var h = addZero(d.getHours(), 2);
  var m = addZero(d.getMinutes(), 2);
  var s = addZero(d.getSeconds(), 2);
  var ms = addZero(d.getMilliseconds(), 3);
  return h + ":" + m + ":" + s + ":" + ms;
}
defineExpose({
  callAction
});
</script>
<style lang="scss" scoped>
.dimensional-map {
  // width: 100vw;
  // height: 56.25vw;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: -500;

  iframe {
    width: 100%;
    height: 100%;
  }
}
</style>
