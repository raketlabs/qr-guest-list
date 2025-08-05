<script setup>
import Registration from '@/components/Registration.vue';
import Confirmation from '@/components/Confirmation.vue';
import Print from '@/components/Print.vue';

const page = window.location.hash.substring(1);
</script>
<template>
  <Registration v-if="page === ``"></Registration>
  <Confirmation v-if="page === `scan`"></Confirmation>
  <Print v-if="page === `print`"></Print>
</template>

<style scoped>
#end-form {
  margin: 20px auto;
}

#qr {
  margin: 20px auto;
  width: 256px;
}
</style>
