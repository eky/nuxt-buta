<template>
  <span ref="slot" role="presentation" class="🔄" :style="cssVars">
    <slot></slot>
  </span>
</template>

<style scoped>
.🔄 {
  display: inline-block;
  font-size: var(--size);
  transform: rotateZ(-360deg);
  animation: do-a-barrel-roll var(--duration) linear forwards infinite;
}

@keyframes do-a-barrel-roll {
  100% {
    transform: rotateZ(0deg);
  }
}
</style>

<script>
export default {
  name: 'DoABarrelRoll',
  props: {
    duration: {
      type: String,
      default: '1s',
    },
    size: {
      type: String,
      default: '120px',
    },
  },
  data() {
    return {
      codeContent: '',
    }
  },
  computed: {
    cssVars() {
      return {
        '--duration': this.duration,
        '--size': this.size,
      }
    },
  },
  mounted() {
    const { duration, size } = this
    console.log({ duration, size }, this)
  },
}
</script>
