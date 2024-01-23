<template>
  <div id="box">
    <yorushika-logo id="logo"/>
  </div>
</template>


<script setup>
import YorushikaLogo from "@/components/icons/yorushika-logo.vue";
import {onMounted} from "vue";

onMounted(() => {
  let logo = document.getElementById("logo");
  let box = document.getElementById("box");

  // initial properties of the logo
  let xPos = 100
  let yPos = 100
  let xSpeed = 3
  let ySpeed = 3
  let fps = 60

  setInterval(
      () => {
        // make box full screen
        box.style.height = `${window.innerHeight}px`;
        box.style.width = `${window.innerWidth}px`;

        xPos += xSpeed
        yPos += ySpeed

        // bounce off the walls if it is going to go out of the box
        if (xPos + logo.clientWidth > box.clientWidth) {
          xPos = box.clientWidth - logo.clientWidth
          xSpeed *= -1
        } else if (xPos < 0) {
          xPos = 0
          xSpeed *= -1
        }

        if (yPos + logo.clientHeight > box.clientHeight) {
          yPos = box.clientHeight - logo.clientHeight
          ySpeed *= -1
        } else if (yPos < 0) {
          yPos = 0
          ySpeed *= -1
        }

        // update position
        logo.style.left = `${xPos}px`;
        logo.style.top = `${yPos}px`;
      },
      // 60 FPS
      1000 / fps)
})

</script>
<style scoped>
#box, #logo {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#box {
  position: relative;
}

#logo {
  width: 200px;
  height: 200px;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
