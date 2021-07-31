<template>
  <v-expansion-panels style="width: 640px;" class="ma-5">
    <v-expansion-panel>
      <v-expansion-panel-header>
        Commands
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <div class="text-body mb-5">
          <code>$queue &lt;youtube|twitch|streamable&gt; &lt;id&gt;</code><br />
          Enqueues media from any of the three hosts based on id. Note that the
          id is not the url.
        </div>
        <div class="text-body mb-5">
          <code>$like</code><br />
          Likes current media.
        </div>
        <div class="text-body">
          <code>$dislike</code><br />
          Dislikes current media. If enough dislikes are reached the current
          media will be skipped.
        </div>
      </v-expansion-panel-content>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-header>
        Moderator Commands
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <div class="text-body mb-5">
          <code>$skip</code><br />
          Skips current media.
        </div>
        <div class="text-body mb-5">
          <code>$alert &lt;message&gt;</code><br />
          Sends an alert to all users.
        </div>
      </v-expansion-panel-content>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-header>
        How do I change volume? / Why is it muted?
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <div class="text-body">
          Refer to the GIF below to change volume:
        </div>
        <img src="@/assets/volumeHowTo.gif" alt="volume how to" width="80%" />
      </v-expansion-panel-content>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-header>
        It wont play!
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <div class="text-body mb-5">
          Disable all addblock/similar extensions and refresh the page.
        </div>
        <div class="text-body mb-5">
          Press the
          <v-icon>
            mdi-refresh
          </v-icon>
          button.
        </div>
        <div>
          Try using a different browser.
        </div>
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<script>
export default {};
</script>

<style></style>
