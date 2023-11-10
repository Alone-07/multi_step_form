<script setup lang="ts">
import { ref } from 'vue';
import Sidebar from './components/Sidebar.vue';
import StepContainer from './components/StepContainer.vue'
import Button from './components//Button.vue';
import Thankyou from './components//Thankyou.vue';

const currentStep = ref(0);
const sidebars = ref(['Your info', 'Select plan', 'Add-ons', "Summary"]);
const thankYou = ref(false)

const goBack = () => {
  return currentStep.value <= 0 ? currentStep.value : currentStep.value--;
}
const nextStep = () => {
  return currentStep.value >= sidebars.value.length - 1 ? (currentStep.value, thankYou.value = true) : currentStep.value++;
}

</script>

<template>
  <div class="container">
    <!-- sidebar -->
    <div class="cover" v-show="!thankYou">
      <Sidebar :sidebars="sidebars" :activeStep="currentStep"></Sidebar>
      <StepContainer :current-step="currentStep" />
      <Button @goBack="goBack" @nextStep="nextStep" :current-step="currentStep" :thank-you="thankYou"
        :side-bars="sidebars" />
    </div>
    <Thankyou v-show="thankYou" />
  </div>
</template>

<style scoped lang=scss>
@use './assets/styles/index' as *;


.container {
  width: $min_width;
}
</style>
