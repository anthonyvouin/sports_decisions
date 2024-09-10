<template>
  <div class="d-flex align-items-center bg-primary p-2 rounded">
    <div class="me-2">
      <img src="../../assets/player.png" alt="Avatar" class="rounded-circle bg-white" width="40" height="40" />
    </div>
    <div>
      <div class="fw-bold text-white">{{ props.user.nickname }}</div>
      <div class="text-info">{{ props.user.position }}</div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  user: Object
});
</script>

<style scoped>
*

.bg-primary {
  background-color: #003049 !important;
}

.text-info {
  color : gray !important;
}
</style>