<script setup>
import { GOOGLE_FORMS_URL, PASSWORD } from '@/assets/constants';

function confirm() {
  const password = prompt(`Enter password`);
  if (password === PASSWORD) {
    const googleFormsUrl = new URL(GOOGLE_FORMS_URL);
    googleFormsUrl.search = window.location.search;
    window.location = googleFormsUrl;
  }
};

function print() {
  const password = prompt(`Enter password`);
  if (password === PASSWORD) {
    const googleFormsUrl = new URL(GOOGLE_FORMS_URL);

    for (let param of googleFormsUrl.searchParams) {
      const k = param[0];
      const v = param[1];

      if (v === `Name`) {
        const url = new URL(window.location);
        const guestName = url.searchParams.get(k);

        const printUrl = new URL(window.location);
        printUrl.search = ``;
        printUrl.searchParams.set(`name`, guestName);
        printUrl.hash = `print`;
        window.location = printUrl;
      }
    }
  }
};
</script>

<template>
<div class="row">
<div class="col-12">
    <button id="confirm-button" type="button" class="btn btn-primary w-100" @click="confirm">Confirm Registration</button>
</div>
</div>
<div class="row">
<div class="col-12">
    <button id="print-button" type="button" class="btn btn-success w-100" @click="print">Print Name</button>
</div>
</div>
</template>

<style scoped>
.row {
  margin: 40px;
}
</style>