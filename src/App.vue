<template>
  <main>
    <CronTabConverter />
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronTabConverter from './components/CronTabConverter.vue';

export default defineComponent({
  name: 'App',
  components: {
    CronTabConverter,
  },
});
</script>
