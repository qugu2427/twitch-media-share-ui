<template>
  <iframe
    style="height: 100%;width: 100%;"
    allow="autoplay"
    :src="`https://streamable.com/o/${id}?autoplay=1&loop=0&t=${start}&mute=0`"
    frameborder="0"
  ></iframe>
</template>

<script>
export default {
  props: {
    id: String,
    start: Number,
  },
};
</script>

<style></style>
