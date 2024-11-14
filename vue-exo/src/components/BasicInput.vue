<template>
  <input v-model="inputValue" :type="type" :name="name" :id="name" :required="required">
</template>

<script setup>
import { ref } from 'vue';

defineProps({
  name: String,
  type: String,
  required: Boolean
})

const inputValue = ref('');

</script>