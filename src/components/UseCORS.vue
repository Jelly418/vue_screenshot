<template>
  <div ref="useCORS">
    <img :src="imageUrl + '?' + new Date().getTime()" crossOrigin="anonymous" />
    <div @click="generatorImageuseCORS" class="img-btn">生成图片</div>
  </div>
</template>
<script>
import html2canvas from "html2canvas";
export default {
  name: "UserCORS",
  data() {
    return {
      imageUrl:
        "https://user-gold-cdn.xitu.io/2018/12/18/167c06ce8cf413d1?w=476&h=260&f=webp&s=11552", // 跨域地址
      screenshotImage: "" // 保存的base64地址
    };
  },
  methods: {
    async generatorImageuseCORS() {
      const opts = {
        useCORS: true
      };
      // const ele = this.$refs.img;
      const canvas = await html2canvas(this.$refs.img, opts);
      this.screenshotImage = canvas.toDataURL("image/jpg");
    }
  }
};
</script>
// 解决跨域最常用的方法是跨域资源共享，我们将图片服务器的response header设置 //
access-control-allow-origin: *
