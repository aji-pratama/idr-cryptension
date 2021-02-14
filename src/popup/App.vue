<template>
  <card-counter time="This is Time" />
</template>

<script>
import CardCounter from '@/components/CardCounter.vue'

export default {
  name: 'App',
  components: { CardCounter }
}
</script>

<style>
html {
  width: 400px;
  height: 400px;
}
</style>
