<script setup lang="ts">
import { computed } from 'vue'
const props = defineProps(['selectedPlan', 'activePlan', 'selectedFeatures'])
const selectedFeaturesTotal = computed(() => {
  return props.selectedFeatures.reduce((total, { price }) => total + price, 0)
})

</script>

<template>
  <div>
    <h1 class="head">Finishing up</h1>
    <p class="text">Double-check eveything looks OK before confirming</p>
    <div class="card">
      <div class="selected_plan_container">
        <div class="plan_container">
          <p class="plan_name">{{ props.selectedPlan[0]?.title }} ({{ props.activePlan.name }})</p>
          <p class="change">Change</p>
        </div>
        <p class="price">${{ props.selectedPlan[0]?.price }}/{{ props.activePlan.name == 'Monthly' ? 'mo' : 'yr' }}</p>
      </div>
      <div class="additional_feature_container">
        <p class="additional_feature" v-for="{ feature, priceText } in props.selectedFeatures">
          <span class="feature_title">{{ feature }}</span>
          <span class="feature_price">{{ priceText }}</span>
        </p>
      </div>
      <div class="total_container">
        <p class="total_text">Total (per {{ props.activePlan.name == 'Monthly' ? 'mo' : 'yr' }})</p>
        <p class="total_price">+${{ selectedPlan[0]?.price + selectedFeaturesTotal }}/{{ props.activePlan.name == 'Monthly'
          ? 'mo' : 'yr' }}</p>
      </div>
    </div>
  </div>
</template>


<style lang="scss" scoped ></style>
