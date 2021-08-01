<template>
  <v-card class="ma-5" style="width: 640px;">
    <!-- top bar -->
    <div class="text-button text-truncate pa-3">
      <v-icon left>mdi-play</v-icon>
      {{ media.title }}
    </div>

    <!-- <div
      v-if="overlay"
      style="height: 360px;width: 640px;margin-bottom: -300px;background-color: purple;z-index: 10;"
    ></div> -->

    <div :style="overlay ? 'pointer-events: none;' : ''">
      <div style="height: 360px;background-color: black;">
        <youtube
          v-if="media.host == 'youtube'"
          :id="media.id"
          :start="media.start"
        />
        <twitch
          v-else-if="media.host == 'twitch'"
          :id="media.id"
          :start="media.start"
        />
        <streamable
          v-else-if="media.host == 'streamable'"
          :id="media.id"
          :start="media.start"
        />
      </div>
    </div>

    <!-- player bar -->
    <div class="d-flex justify-space-between align-center">
      <div class="d-flex pl-4">
        <div class="text-button mr-3">
          <v-icon left>
            mdi-thumb-up
          </v-icon>
          {{ likes }}
        </div>
        <div class="text-button ml-3">
          {{ dislikes }}
          <v-icon right>
            mdi-thumb-down
          </v-icon>
        </div>
      </div>
      <div class="text-body">
        {{ formatSeconds(this.secondsElapsed) }} /
        {{ formatSeconds(media.duration) }}
      </div>
      <div>
        <v-btn fab tile text @click="overlay = !overlay">
          <v-icon>
            {{ overlay ? "mdi-shield-off-outline" : "mdi-shield" }}
          </v-icon>
        </v-btn>
        <v-btn fab tile text @click="$emit('refresh', secondsElapsed)">
          <v-icon>
            mdi-refresh
          </v-icon>
        </v-btn>
      </div>
    </div>
    <v-alert
      tile
      dense
      type="error"
      dark
      color="transparent"
      v-show="!overlay"
      class="ma-1 pa-3"
    >
      Anti-click overlay is disabled.
    </v-alert>
  </v-card>
</template>

<script>
import Youtube from "./Youtube.vue";
import Twitch from "./Twitch.vue";
import Streamable from "./Streamable.vue";
export default {
  components: {
    Streamable,
    Youtube,
    Twitch,
  },
  props: {
    media: Object,
    likes: Number,
    dislikes: Number,
  },
  data() {
    return {
      overlay: true,
      secondsElapsed: 0,
    };
  },
  methods: {
    formatSeconds(seconds) {
      let nhours = Math.floor(((seconds % 31536000) % 86400) / 3600);
      let nminutes = Math.floor((((seconds % 31536000) % 86400) % 3600) / 60);
      let nseconds = (((seconds % 31536000) % 86400) % 3600) % 60;
      let fhours = nhours > 0 ? nhours + ":" : "";
      let fminutes = nhours > 0 && nminutes < 10 ? "0" + nminutes : nminutes;
      let fseconds = nseconds < 10 ? "0" + nseconds : nseconds;
      return `${fhours}${fminutes}:${fseconds}`;
    },
  },
  mounted() {
    setInterval(() => {
      if (!(this.secondsElapsed >= this.media.duration)) {
        this.secondsElapsed++;
      }
    }, 1000);
  },
  watch: {
    media() {
      this.secondsElapsed = this.media.start;
    },
  },
};
</script>

<style></style>
