<template>
  <div id="box">
    <img id="logo" src="@/assets/yorushika.svg" alt=""/>
  </div>
  <!--<button @click="toggleFullscreen">Toggle Fullscreen</button>-->
</template>


<script setup>
import {onMounted} from "vue";
import yorushika from "@/assets/yorushika.svg";
import zutomayo from "@/assets/zutomayo.svg";
import yoasobi from "@/assets/yoasobi.svg";

// function toggleFullscreen() {
//   let doc = window.document;
//   let docEl = doc.documentElement;
//
//   let requestFullScreen = docEl.requestFullscreen || docEl.mozRequestFullScreen || docEl.webkitRequestFullScreen || docEl.msRequestFullscreen;
//   let cancelFullScreen = doc.exitFullscreen || doc.mozCancelFullScreen || doc.webkitExitFullscreen || doc.msExitFullscreen;
//
//   if (!doc.fullscreenElement && !doc.mozFullScreenElement && !doc.webkitFullscreenElement && !doc.msFullscreenElement) {
//     requestFullScreen.call(docEl);
//   } else {
//     cancelFullScreen.call(doc);
//   }
// }

let logos = [
  yorushika,
  zutomayo,
  yoasobi,
];
let currentLogoIndex = 1

function switchLogo() {
  let logo = document.getElementById("logo");
  logo.src = logos[currentLogoIndex++ % logos.length]
  console.log(currentLogoIndex)
}

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
          switchLogo()
        } else if (xPos < 0) {
          xPos = 0
          xSpeed *= -1
          switchLogo()
        }

        if (yPos + logo.clientHeight > box.clientHeight) {
          yPos = box.clientHeight - logo.clientHeight
          ySpeed *= -1
          switchLogo()
        } else if (yPos < 0) {
          yPos = 0
          ySpeed *= -1
          switchLogo()
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
  position: absolute;
  top: 0;
  left: 0;
  width: 200px;
  height: 200px;
}
</style>
