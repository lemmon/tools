<script>
const size = 20;
const weight = 1.5;
</script>

<svg
  class="container"
  height={size}
  width={size}
  viewBox="0 0 {size} {size}"
  fill="none"
  stroke="currentColor"
  stroke-width={weight}
  stroke-linecap="round"
>
  <circle class="car" cx={size / 2} cy={size / 2} r={size / 2 - weight / 2} pathlength="100" />
</svg>

<style>
.container {
  --speed: 2s;
  transform-origin: center;
  animation: rotate var(--speed) linear infinite;
  will-change: transform;
  overflow: visible;
}

.car {
  stroke-dasharray: 1, 200;
  stroke-dashoffset: 0;
  animation: stretch calc(var(--speed) * 0.75) ease-in-out infinite;
  will-change: stroke-dasharray, stroke-dashoffset;
  transition: stroke 0.5s ease;
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}

@keyframes stretch {
  0% {
    stroke-dasharray: 0, 150;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 75, 150;
    stroke-dashoffset: -25;
  }
  100% {
    stroke-dashoffset: -100;
  }
}
</style>
