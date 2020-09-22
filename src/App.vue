<template>
  <div id="app">
    <div ref="simpledDemo">
      <img ref="capture" alt="Vue logo" src="./assets/logo.png" />
      <div>
        <input type="button" value="截图" @click="generatorImage()" />
      </div>
    </div>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <UserCORS></UserCORS>
    <QRCode></QRCode>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import html2canvas from "html2canvas";
import UserCORS from "./components/UseCORS.vue";
import QRCode from "./components/QRCode.vue";

export default {
  name: "App",
  components: {
    // HelloWorld
    UserCORS,
    QRCode
  },
  methods: {
    generatorImage() {
      html2canvas(this.$refs.capture).then(canvas => {
        this.$refs.simpledDemo.append(canvas);
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

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
