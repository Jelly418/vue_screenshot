<template>
  <div class="main">
    <div class="screenshot_area">
      <p>扫一扫</p>
      <img src="../assets/QRCode.png" />
    </div>
    <div class="copy">
      <button @click="copy()">截图</button>
    </div>
  </div>
</template>
<script>
import html2canvas from "html2canvas";
export default {
  name: "QRCode",
  data() {
    return {};
  },
  methods: {
    copy() {
      var canvas2 = document.createElement("canvas");
      let _canvas = document.querySelector(".screenshot_area");
      var w = parseInt(window.getComputedStyle(_canvas).width);
      var h = parseInt(window.getComputedStyle(_canvas).height);
      //将canvas画布放大若干倍，然后盛放在较小的容器内，就显得不模糊了
      canvas2.width = w * 2;
      canvas2.height = h * 2;
      canvas2.style.width = w + "px";
      canvas2.style.height = h + "px";
      //可以按照自己的需求，对context的参数修改,translate指的是偏移量
      var context = canvas2.getContext("2d");
      context.scale(2, 2);
      html2canvas(document.querySelector(".screenshot_area"), {
        canvas: canvas2
      }).then(function(canvas) {
        document.querySelector(".main").appendChild(canvas);
        let link = document.createElement("a");
        link.href = canvas.toDataURL();
        link.setAttribute("download", "图片canvas.png");
        link.style.display = "none";
        document.body.appendChild(link);
        link.click();
      });
    }
  }
};
</script>
