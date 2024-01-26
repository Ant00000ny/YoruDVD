<template>
  <div id="box">
    <yorushika id="logo" :fill-color="currentColor"/>
  </div>
  <!--<button @click="toggleFullscreen">Toggle Fullscreen</button>-->
</template>


<script setup>
import {onMounted, reactive, ref} from "vue";
import Yorushika from "@/logo/yorushika.vue";

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

// let logos = [
//   yorushika,
//   zutomayo,
//   yoasobi,
// ];
// let currentLogoIndex = 1
//
// function switchLogo() {
//   let logo = document.getElementById("logo");
//   logo.src = logos[currentLogoIndex++ % logos.length]
// }

let colors = [
  "#FF0000",
  "#FF7F00",
  "#FFFF00",
  "#00FF00",
  "#0000FF",
  "#8F00FF",
  "#FF00FF",
    "#FFFFFF"
]
let currentColorIndex = 0
let currentColor = ref(colors[currentColorIndex])

function switchColor() {
  currentColor.value = colors[++currentColorIndex % colors.length]
}

onMounted(() => {
  let logo = document.getElementById("logo");
  let box = document.getElementById("box");

  // initial properties of the logo
  let xPos = 100
  let yPos = 100
  let xSpeed = 5
  let ySpeed = 5
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
          // switchLogo()
          switchColor()
        } else if (xPos < 0) {
          xPos = 0
          xSpeed *= -1
          // switchLogo()
          switchColor()
        }

        if (yPos + logo.clientHeight > box.clientHeight) {
          yPos = box.clientHeight - logo.clientHeight
          ySpeed *= -1
          // switchLogo()
          switchColor()
        } else if (yPos < 0) {
          yPos = 0
          ySpeed *= -1
          // switchLogo()
          switchColor()
        }

        // update position
        logo.style.left = `${xPos}px`;
        logo.style.top = `${yPos}px`;
      },
      // 60 FPS
      1000 / fps
  )
})

</script>
<style scoped>
#box, #logo {
  box-sizing: border-box;
}

#box {
  position: relative;
  background-color: #171515;
}

#logo {
  position: absolute;
  top: 0;
  left: 0;
  width: 200px;
  height: 200px;
}
</style>
