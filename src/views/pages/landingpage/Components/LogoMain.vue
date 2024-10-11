<template>
  <div class="logo">
    <RouterLink to="/" aria-label="logo">
      <img height="50px" src="https://onboardingdemo.s3.us-east-2.amazonaws.com/datapoint.png" />
    </RouterLink>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import { RouterLink } from 'vue-router';
const primary = ref('rgb(var(--v-theme-primary))');
</script>
