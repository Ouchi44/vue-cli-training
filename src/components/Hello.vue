<template>
  <p class="message">これはHello: {{ msg }}</p>
</template>

<style>
.message { color: #42b983; }
</style>

<script>
export default {
  props: {
    msg: {
      type: String,
      default: 'こんにちは！'
    }
  }
}
</script>
