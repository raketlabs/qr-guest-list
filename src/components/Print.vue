<script setup>
const params = new URLSearchParams(window.location.search);
const guestName = params.get(`name`);
</script>

<template>
<div id="guest-name">{{ guestName }}</div>
</template>

<style scoped>
#guest-name {
  text-align: center;
  font-size: 64pt;
}
</style>