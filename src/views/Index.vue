<template>
  <v-container class="d-flex flex-column align-center">
    <v-alert
      dark
      color="red"
      icon="mdi-bullhorn"
      prominent
      v-if="showAlert"
      class="ma-5"
      style="width: 640px;"
    >
      <v-row align="center">
        <v-col class="font-weight-bold grow">
          {{ alertMessage }}
        </v-col>
        <v-col class="shrink" @click="showAlert = false">
          <v-btn depressed>got it</v-btn>
        </v-col>
      </v-row>
    </v-alert>

    <v-alert
      outlined
      color="white"
      dense
      style="width: 640px;"
      v-if="showRefreshInfo"
      class="ma-5"
    >
      <v-row align="center">
        <v-col class="grow">
          If the video is paused press
          <v-icon>mdi-refresh</v-icon>
        </v-col>
        <v-col class="shrink" @click="showRefreshInfo = false">
          <v-btn text>got it</v-btn>
        </v-col>
      </v-row>
    </v-alert>

    <Player
      :media="media"
      :likes="likes"
      :dislikes="dislikes"
      @refresh="refresh"
    />
    <Queue :queue="queue" />
    <Dropdowns />
    <p>
      © 2021 Tencent 腾讯 -
      <a
        href="https://github.com/qugu2427/twitch-media-share-ui"
        style="color: white;opacity: 0.5;"
        >Github</a
      >
    </p>
  </v-container>
</template>

<script>
import Player from "@/components/Player.vue";
import Queue from "@/components/Queue.vue";
import Dropdowns from "@/components/Dropdowns.vue";
export default {
  components: {
    Player,
    Queue,
    Dropdowns,
  },
  data() {
    return {
      media: { host: "youtube", id: "", duration: 0, start: 0 },
      queue: [],
      likes: 0,
      dislikes: 0,
      showAlert: false,
      alertMessage: "",
      showRefreshInfo: true,
    };
  },
  methods: {
    refresh(secondsElapsed) {
      this.media.start = secondsElapsed;
    },
  },
  sockets: {
    connect() {
      console.log("connected to socket");
    },
    play(media) {
      console.log("play");
      console.log(media);
      this.media = media;
      this.queue.shift();
      this.likes = 0;
      this.dislikes = 0;
      this.media.duration = Math.ceil(this.media.duration);
    },
    enqueue(media) {
      console.log("enqueue");
      console.log(media);
      this.queue.push(media);
    },
    setQueue(queue) {
      console.log("queue");
      console.log(queue);
      this.queue = queue;
    },
    alert(message) {
      this.alertMessage = message;
      this.showAlert = true;
    },
    setVotes(obj) {
      this.likes = obj.likes;
      this.dislikes = obj.dislikes;
    },
  },
};
</script>

<style></style>
