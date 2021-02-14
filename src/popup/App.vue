<template>
  <card-counter v-bind:time="waktu" />
</template>

<script>
import CardCounter from '@/components/CardCounter.vue'

export default {
  name: 'App',
  components: { CardCounter },
  data: {
    waktu: "Ini adalah waktu"
  }
}
</script>

<style>
html {
  width: 400px;
  height: 400px;
}
</style>
