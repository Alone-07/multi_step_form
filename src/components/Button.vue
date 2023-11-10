<script setup lang="ts">
const emit = defineEmits(['goBack', 'nextStep'])
const props = defineProps({
  currentStep: Number,
  thankYou: Boolean,
  sideBars: Array,
})
</script>
<template>
  <div class="btn_container">
    <button type="button" @click="emit('goBack')">Go Back</button>
    <button type="button" @click="emit('nextStep')">{{ currentStep == sideBars.length - 1 ? 'Confirm' : `Next
      Step`}}</button>
  </div>
</template>
<style lang="scss" scoped>
button {
  padding: 0.5rem;
  border-radius: 5px;
  outline: none;
}
</style>
