<template>
  <div id="app">
    <BMICalc />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BMICalc from './components/BMICalc.vue';

export default defineComponent({
  components: {
    BMICalc
  }
});
</script>