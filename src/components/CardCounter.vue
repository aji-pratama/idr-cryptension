<template>
  <div>
    <div class="alert alert-success">{{ time }}</div>
  </div>
</template>

<script>
export default {
  name: 'CardCounter',
  props: { 
    time: String
  }
}
</script>

<style scoped>
p {
  font-size: 20px;
}
</style>
