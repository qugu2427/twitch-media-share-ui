<template>
  <iframe
    style="height: 100%;width: 100%;"
    allow="autoplay"
    :src="
      `https://clips.twitch.tv/embed?clip=${id}&parent=www.4weird.org&autoplay=true&time=${start}s`
    "
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
