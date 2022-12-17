<template>
  <div class="torch-container">
    <div class="torch"></div>
    <div class="fire">
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
      <div class="particle"></div>
    </div>

    <div class="tourch__wrapper">
      <img src="../assets/torch.png" alt="" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
img {
  width: 510px;
  height: 710px;
  z-index: -1;
}

.tourch__wrapper {
  width: 510px;
  position: absolute;
  top: 209px;
  left: -199px;
  z-index: -1;
}

$fireColor: rgb(255, 80, 0);
$fireColorT: rgba(255, 80, 0, 0);
$dur: 1s;
$blur: 0.03em;
$fireRad: 3em;
$parts: 50;
$partSize: 5em;

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
html {
  height: 100%;
}

@keyframes glowing {
  from {
    opacity: 0.5;
  }
  50% {
    opacity: 0.9;
  }
  to {
    opacity: 0.5;
  }
}
.torch-container:before {
}
.torch-container {
  position: absolute;
  max-width: 300px;
}
.torch {
  background: url(http://acitjazz.com/images/torch.png) no-repeat;
  width: 144px;
  height: 250px;
  position: absolute;
  left: 50%;
  margin: 0 0 0 -72px;
  top: 0;
}
.fire {
  bottom: 330px;
  z-index: 2;
  left: 0;
  font-size: 36px;
  filter: blur($blur);
  -webkit-filter: blur($blur);
  margin: 3em auto 0 auto;
  width: 270px;
  height: 12em;
}
.particle {
  animation: rise $dur ease-in infinite;
  background-image: radial-gradient($fireColor 20%, $fireColorT 70%);
  border-radius: 50%;
  mix-blend-mode: screen;
  opacity: 0;
  position: absolute;
  bottom: 0;
  width: $partSize;
  height: $partSize;
  // spread particles out in time and x-position to get desired effect
  @for $p from 1 through $parts {
    &:nth-of-type(#{$p}) {
      animation-delay: $dur * random();
      left: calc((100% - #{$partSize}) * #{($p - 1) / $parts});
    }
  }
}
@keyframes rise {
  from {
    opacity: 0;
    transform: translateY(0) scale(1);
  }
  25% {
    opacity: 1;
  }
  to {
    opacity: 0;
    transform: translateY(-10em) scale(0);
  }
}
</style>
