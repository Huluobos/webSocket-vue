<template>
  <div class="hello">

  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        webSocketUrl:"192.168.0.200"
      }
    },
    methods: {
      initWebSocket() { //初始化weosocket
        const wsuri = 'ws://' + this.webSocketUrl;//ws地址
        this.$websocket = new WebSocket(wsuri);
        this.$websocket.onopen = this.websocketonopen;
        this.$websocket.onerror = this.websocketonerror;
        this.$websocket.onmessage = this.websocketonmessage;
        this.$websocket.onclose = this.websocketclose;
      },
      websocketonopen() {
        var that = this
        console.log("WebSocket连接成功");
      },
      websocketonerror(e) { //错误
        console.log("WebSocket连接发生错误");
      },
      websocketonmessage(e) { //数据接收
        var that = this
        const redata = JSON.parse(e.data);
        console.log(redata);
      },
      websocketclose() { //关闭
        console.log("WebSocket连接关闭");
      },
      mounted() {
        var _this = this;
        _this.initWebSocket()  //在合适的时候执行
      },
      beforeDestroy() {
        this.websocketclose();
        //退出登录或者关闭页面时摧毁连接
        //个人实测，在服务端，连接并没有被摧毁
      },
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
