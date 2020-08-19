<template>
  <div class="home">
    <transition-group name="fade">
      <div
        class="banner"
        v-for="(item,i) in source"
        :key="item"
        :src="item"
        v-show="count === i+1"
        :style="`background-image:url(${item})`"
      >
      </div>
    </transition-group>
     <div class="main">
      <the-content></the-content>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import TheContent from '../components/TheContent'
export default {
  
  name: "Home",
  components: {
    TheContent
  },
  data() {
    return {
      count: 1,
      source: [
        require("../assets/1.jpg"),
        require("../assets/2.jpg"),
        require("../assets/3.jpg")
      ]
    };
  },
  mounted() {
    setInterval(() => {
      if (this.count === 3) {
        this.count = 1;
      } else {
        this.count++;
      }
    }, 5000);
  }
};
</script>
<style scoped>
.banner {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-position: 50%;
  background-size: contain;
  z-index: -1;
  color: #fff;
  text-shadow: 12px 12px 3px rgba(0, 0, 0, 0.1);
  padding-left: 1em;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
  background-position: 100%;
}

.fade-enter-active,
.fade-leave-active {
  transition: 1s;
}
.main {
  background: #fff;
  margin-top: 100vh;
  min-height: 120vh;
}
</style>
