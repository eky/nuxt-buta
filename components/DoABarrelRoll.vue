<template>
  <span
    ref="slot"
    role="presentation"
    class="🔄"
    :style="cssVars"
    @click="clicked"
  >
    <slot></slot>
  </span>
</template>

<style scoped>
.🔄 {
  display: inline-block;
  font-size: var(--font-size);
  cursor: pointer;
  user-select: none;
  transform: rotateZ(-360deg);
  animation: do-a-barrel-roll var(--duration) linear forwards infinite;
  animation-play-state: var(--animation-play-state);
}

@keyframes do-a-barrel-roll {
  100% {
    transform: rotateZ(0deg);
  }
}
</style>

<script>
const props = {
  duration: {
    type: String,
    default: '1s',
  },
  size: {
    type: Number,
    default: 120,
  },
}

const data = () => ({
  isAnimationPlaying: false,
})

const computed = {
  cssVars() {
    const { size, isAnimationPlaying } = this
    const fontSize = size * 0.7
    return {
      '--duration': this.duration,
      '--font-size': `${fontSize}px`,
      '--animation-play-state': isAnimationPlaying ? 'paused' : 'running',
    }
  },
}

const methods = {
  clicked(event) {
    this.isAnimationPlaying = !this.isAnimationPlaying
    console.log(
      `${this.$refs.slot.textContent} clicked! ${
        this.isAnimationPlaying ? 'stop' : 'resume'
      }`
    )
  },
}

export default {
  name: 'DoABarrelRoll',
  props,
  data,
  computed,
  mounted() {
    const { duration, size } = this
    console.log(this.$refs.slot.textContent, { duration, size })
  },
  methods,
}
</script>
