<template>
  <v-card
    class="ma-5 d-flex flex-column"
    style="width: 640px;max-height: 220px;"
  >
    <div class="text-button text-truncate pa-3">
      <v-icon left>mdi-tray-full</v-icon>
      queue {{ queue.length }}/25
    </div>
    <v-list class="overflow-y-auto">
      <v-list-item v-for="(item, index) in queue" :key="item.title + index">
        <v-list-item-avatar size="24" color="transparent">
          <v-icon v-if="item.host == 'youtube'" color="#FF0000">
            mdi-youtube
          </v-icon>
          <v-icon v-else-if="item.host == 'twitch'" color="#6441A4">
            mdi-twitch
          </v-icon>
          <v-icon v-else-if="item.host == 'streamable'" color="#0f90fa">
            mdi-infinity
          </v-icon>
        </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title>
            <a
              :href="urlFromHost(item.host) + item.id"
              style="text-decoration: none; color: inherit;"
              onmouseover="style='text-decoration: underline;color: inherit;'"
              onmouseout="style='text-decoration: none; color: inherit;'"
              target="_blank"
            >
              {{ item.title }}
            </a>
          </v-list-item-title>
          <v-list-item-subtitle>{{ item.addedBy }}</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-card>
</template>

<script>
export default {
  props: {
    queue: Array,
  },
  methods: {
    urlFromHost(host) {
      if (host == "youtube") {
        return "https://www.youtube.com/watch?v=";
      } else if (host == "twitch") {
        return "https://clips.twitch.tv/";
      } else if (host == "streamable") {
        return "https://streamable.com/";
      }
    },
  },
};
</script>

<style></style>
