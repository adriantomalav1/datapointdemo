<script setup lang="ts">
import { shallowRef } from 'vue';

const footerLink = shallowRef([
  {
    title: 'Home',
    link: 'https://ableproadmin.com/vue/'
  },
  {
    title: 'Documentation',
    link: 'https://phoenixcoded.gitbook.io/able-pro'
  },
  {
    title: 'Support',
    link: 'https://phoenixcoded.authordesk.app/'
  }
]);
</script>
<template>
  <v-footer class="px-0 footer">
    <v-row justify="center" no-gutters>
      <v-col cols="6">
        <p v-if="false" class="text-caption mb-0">© Plexus ♥ crafted by Team Datapoint</p>
      </v-col>
      <v-col class="text-end" cols="6">
        <a v-for="(item, i) in footerLink" :key="i" class="mx-2 text-caption text-darkText" target="_blank" :href="item.link">
          {{ item.title }}
        </a>
      </v-col>
    </v-row>
  </v-footer>
</template>
