<script setup lang="ts">
import { ref, computed, watch } from 'vue'
import Step1 from './Step1.vue'
import Step2 from './Step2.vue'
import Step3 from './Step3.vue'
import Step4 from './Step4.vue'
const props = defineProps(['currentStep'])

const personalInfo = ref({
  name: null,
  email: null,
  phone: null,
})
const plan = ref({
  monthly: {
    name: 'Monthly',
    enabled: true,
    availablePlans: [{ title: 'Arcade', price: 9, selected: false }, { title: 'Advanced', price: 12, selected: false }, { title: 'Pro', price: 15, selected: false }],
    free: null,
  },
  yearly: {
    name: 'Yearly',
    enabled: false,
    availablePlans: [{ title: 'Arcade', price: 90, selected: false }, { title: 'Advanced', price: 120, selected: false }, { title: 'Pro', price: 150, selected: false }],
    free: '2 months free',
  }
})
const addOns = ref([
  { feature: 'online service', description: 'Access to multiplayer games', enabled: false, get planPriceName() { return plan.value.monthly.enabled ? 'priceMonth' : 'priceYear' }, priceMonth: 1, priceYear: 10, get price() { return this[this.planPriceName] }, get priceText() { return this.planPriceName == 'priceMonth' ? `+${this.price}/mo` : `+${this.price}/yr` } },
  { feature: 'large storage', description: 'Extra 1TB of cloud save', enabled: false, get planPriceName() { return plan.value.monthly.enabled ? 'priceMonth' : 'priceYear' }, priceMonth: 2, priceYear: 20, get price() { return this[this.planPriceName] }, get priceText() { return this.planPriceName == 'priceMonth' ? `+${this.price}/mo` : `+${this.price}/yr` } },
  { feature: 'customizable profile', description: 'Custom theme on your profile', enabled: false, get planPriceName() { return plan.value.monthly.enabled ? 'priceMonth' : 'priceYear' }, priceMonth: 2, priceYear: 20, get price() { return this[this.planPriceName] }, get priceText() { return this.planPriceName == 'priceMonth' ? `+${this.price}/mo` : `+${this.price}/yr` } }
])

const activePlan = computed(() => plan.value.monthly.enabled == true ? plan.value.monthly : plan.value.yearly);
const selectedPlan = computed(() => activePlan.value.availablePlans.filter(({ selected }) => selected == true))

const selectedFeatures = computed(() => addOns.value.filter(({ enabled }) => enabled == true))

</script>
<template>
  <div class="step_container">
    <Step1 v-show="props.currentStep == 0" v-model:name="personalInfo.name" v-model:email="personalInfo.email"
      v-model:phone="personalInfo.phone" />
    <Step2 v-show="props.currentStep == 1" :plan="plan" />
    <Step3 v-show="props.currentStep == 2" :add-ons="addOns" />
    <Step4 v-show="props.currentStep == 3" :selected-plan="selectedPlan" :active-plan="activePlan"
      :selected-features="selectedFeatures" />
  </div>
</template>
<style lang=scss scoped></style>
