<script setup>
import { ref, useTemplateRef } from 'vue';
import { GOOGLE_FORMS_URL } from '@/assets/constants';

let submitted = ref(false);

const confirmUrl = new URL(window.location);
const googleFormsUrl = new URL(GOOGLE_FORMS_URL);

const qrEl = useTemplateRef(`qr`);
const inputList = useTemplateRef(`input`);

const params = [];

for (let param of googleFormsUrl.searchParams) {
  const k = param[0];
  const v = param[1];

  if (!k.startsWith(`entry`)) {
      continue;
  }

  params.push(param);
}

function generateQr() {

  for (let input of inputList.value) {
      const k = input.id;
      const v = input.value;
      googleFormsUrl.searchParams.set(k, v);
  }

  confirmUrl.search = googleFormsUrl.search;
  confirmUrl.hash = `scan`;

  qrEl.value.innerHTML = ``;
  const qrParams = {
    text: `${confirmUrl}`
  };

  const qr = new QRCode(qrEl.value, qrParams);

  submitted.value = true;
}

</script>

<template>
<div id="qr" ref="qr"></div>
<div class="row" >
  <div class="col-lg-4 col-md-12" v-for="param in params">
    <label :for="param[0]">{{ param[1] }}</label>
    <input type="text" class="form-control" :name="param[0]" :id="param[0]" :disabled="submitted" ref="input">
  </div>
</div>

<div id="end-form"></div>

<div class="row" v-if="!submitted">
  <div class="col-12">
    <button class="btn btn-primary" type="submit" @click="generateQr">Submit</button>
  </div>
</div>
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
