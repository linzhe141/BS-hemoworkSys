<template>
  <canvas 
    width="650px"
    height="700px"
    class="hwImgCanvas"
    id="hwImgCanvas"
  ></canvas>
</template>
<script>
import $ from "jquery";
export default {
  props: ["data"],
  data() {
    return {
      test: "aaa"
    };
  },
  mounted() {
    console.log("fdasfd");
    console.log('el-dialog  ',$('.dev-el-dialog .el-dialog').css('margin-top').split('px')[0])
    var canvas = document.getElementById("hwImgCanvas");
    console.log("canvas-->", canvas);
    console.log($(canvas));
   // if (canvas == null) return false;
    var context = canvas.getContext("2d");
    context.strokeStyle = "red";
    //标记开始书写
    var start = false;
    $(canvas).mousemove(function(event) {
        
      let x = event.pageX - ($('.dev-el-dialog .el-dialog').css('margin-left').split('px')[0]);
      let y = event.pageY + $('.dev-el-dialog').scrollTop() - (parseInt(($('.dev-el-dialog .el-dialog').css('margin-top').split('px')[0]))+80);
      // console.log(x,y)

      if (start) {
        context.lineTo(x, y);
        context.stroke();
      }
    });
    //鼠标按下，开始书写
    $(canvas).mousedown(function(event) {
      console.log(event)
      console.log('scrollTop',$('.dev-el-dialog').scrollTop())
      let x = event.pageX - ($('.dev-el-dialog .el-dialog').css('margin-left').split('px')[0]);
      let y = event.pageY + $('.dev-el-dialog').scrollTop() - (parseInt(($('.dev-el-dialog .el-dialog').css('margin-top').split('px')[0]))+80);
      context.beginPath();
      context.moveTo(x, y);
      console.log(x,y)
      // context.moveTo(88, 20);
      start = true;
    });
    //鼠标抬起，结束书写
    $(canvas).mouseup(function() {
      start = false;
      context.closePath();
    });
  },
  methods: {
      
  }
};
</script>
<style lang="scss" scoped>
.hwImg,
.hwImgCanvas {
  // max-width: 100%;
  // min-width: 100%;
  // min-width: 300px;
  background-size: 100% 100%;
}

</style>