<template>
  <!--<div style="text-align: center; margin-top: 50px">-->
  <!--{{time}} 秒后将为您跳转到 github/wendux-->
  <!--</div>-->
  <div style="position: relative">
    <canvas id="canvas"></canvas>
    <div style="position: absolute; top:5px; right: 10px; z-index: 2; font-size: 16px" id="nav-t" class="hidden-xs-only">
      <v-btn  icon href="https://github.com/CharmingGeeker"><v-icon>fa-github</v-icon></v-btn>
      <v-btn  icon href="https://www.jianshu.com/u/ad08697c889b"><v-icon>more_vert</v-icon></v-btn>
    </div>
    <div style="position: absolute; top:0;left: 0; width: 100%; text-align: center; color: #333; font-size: 16px">
      <div style="height: 3px; background:-webkit-linear-gradient(left,deepskyblue,cornflowerblue)"></div>
      <img src="~@/assets/me.jpeg" style="width: 80px; border-radius: 40px; margin-top: 15vh"/>
      <div style="margin-top: 10px; line-height: 1.7em "><b>唯有深入，方能浅出</b><br><br>我是梁旭，欢迎大家关注我</div>
      <div style="padding: 10px 0;" class="hidden-sm-and-up">
        <a href="https://www.jianshu.com/u/ad08697c889b" style="margin-right: 16px">Blog</a>
        <a href="https://github.com/CharmingGeeker">Github</a>
      </div>
      <div style="padding: 10px 0;" id="tag" class="hidden-xs-only">
        <a href="https://github.com/CharmingGeeker">Github</a>
      </div>
    </div>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  scoped lang="stylus">
  $themeColor=rgb(25,118,210);
  #nav-t{
    a{
      color:$themeColor;
    }
  }
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: rgba( 25, 118, 210, .7);
  }

  a:hover {
    color: rgba( 25, 118, 210, 1);
  }

  #tag a {
    display: inline-block;
    font-size: 15px;
    height: 30px;
    line-height: 30px;
    padding: 0 15px;
    background: rgba(25, 118, 210, .8);
    border-radius: 15px;
    color: white;
    margin-top: 20px;
    margin-left: 16px;
    box-shadow: 0px 0px 2px $themeColor;
    text-decoration none
    transition: all .3s;
  }

  #tag a:hover {
    background: rgba(25, 118, 210, 1);
    box-shadow: 0px 0px 10px $themeColor;
    transform: translate3d(0,-2px,0);
  }

</style>

<script>
  export default {
    name: 'hello',
    mounted() {
      window.requestAnimFrame = function () {
        return window.requestAnimationFrame || window.webkitRequestAnimationFrame || window.mozRequestAnimationFrame || function (callback) {
          window.setTimeout(callback, 1000 / 60);
        };
      }();

      var step = 0;
      //定义三条不同波浪的颜色
      var lines = [

        //"rgba(19, 94, 148, .8)",
        "rgba(33,150,243, .9  )",
        "rgba(25,118,210, .9)",
      ];
      var text1 = $(".text1");

      function loop() {
        var canvas = document.getElementById('canvas');
        var ctx = canvas.getContext('2d');
        var height = document.body.offsetHeight;
        canvas.width = document.body.offsetWidth;
        canvas.height = height;
        ctx.clearRect(0, 0, canvas.width, height);
        // 波浪大小
        var boHeight = height / 20;
        var posHeight = height / 1.3;
        //初始角度为0
        step++;
        for (var j = lines.length - 1; j >= 0; j--) {
          ctx.fillStyle = lines[j];
          //每个矩形的角度都不同，每个之间相差45度
          var angle = (step + j * 50) * Math.PI / 120;
          var deltaHeight = Math.sin(angle) * boHeight;
          var deltaHeightRight = Math.cos(angle) * boHeight;
          ctx.beginPath();
          ctx.moveTo(0, posHeight + deltaHeight);
          ctx.bezierCurveTo(canvas.width / 2, posHeight + deltaHeight - boHeight, canvas.width / 2, posHeight + deltaHeightRight - boHeight, canvas.width, posHeight + deltaHeightRight);
          ctx.lineTo(canvas.width, canvas.height);
          ctx.lineTo(0, canvas.height);
          ctx.lineTo(0, posHeight + deltaHeight);
          ctx.closePath();
          ctx.fill();
        }
        requestAnimFrame(loop);
      }

      loop();
    },
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        time: 5
      }
    }
  }
</script>


