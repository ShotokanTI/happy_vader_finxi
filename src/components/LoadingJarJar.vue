<template>
    <img
    class="animation"
      style="border-radius: 9999px"
      width="150px"
      src="https://media3.giphy.com/media/Fs9cN5byWCZri/giphy.gif"
      alt=""
    />
</template>

<script>
export default {};
</script>

<style>
@keyframes loading {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}
.animation {
  animation: loading 2s linear infinite;
}
</style>